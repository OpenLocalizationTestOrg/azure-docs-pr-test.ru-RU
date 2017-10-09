## <a name="view-device-telemetry-in-hello-dashboard"></a><span data-ttu-id="bf690-101">Представление устройства телеметрии на панели мониторинга hello</span><span class="sxs-lookup"><span data-stu-id="bf690-101">View device telemetry in hello dashboard</span></span>
<span data-ttu-id="bf690-102">панель мониторинга Hello в hello удаленное наблюдение позволяет вам tooview hello телеметрии вашего устройства отправляют tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="bf690-102">hello dashboard in hello remote monitoring solution enables you tooview hello telemetry your devices send tooIoT Hub.</span></span>

1. <span data-ttu-id="bf690-103">В браузере, возвращаемого toohello удаленного решений мониторинга, щелкните **устройств** в hello левую панель toonavigate toohello **список устройств**.</span><span class="sxs-lookup"><span data-stu-id="bf690-103">In your browser, return toohello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="bf690-104">В hello **список устройств**, вы увидите, что находится в состоянии hello устройства **под управлением**.</span><span class="sxs-lookup"><span data-stu-id="bf690-104">In hello **Devices list**, you should see that hello status of your device is **Running**.</span></span> <span data-ttu-id="bf690-105">Если нет, нажмите **включить устройство** в hello **сведений об устройстве** панель.</span><span class="sxs-lookup"><span data-stu-id="bf690-105">If not, click **Enable Device** in hello **Device Details** panel.</span></span>
   
    ![Просмотр состояния устройства][18]
3. <span data-ttu-id="bf690-107">Нажмите кнопку **мониторинга** tooreturn toohello панели мониторинга, выберите устройство в hello **tooView устройства** tooview раскрывающийся список его телеметрии.</span><span class="sxs-lookup"><span data-stu-id="bf690-107">Click **Dashboard** tooreturn toohello dashboard, select your device in hello **Device tooView** drop-down tooview its telemetry.</span></span> <span data-ttu-id="bf690-108">Hello телеметрии из образца приложения hello — 50 единиц для температура, 55 единицы измерения для температура и 50 единиц для влажности.</span><span class="sxs-lookup"><span data-stu-id="bf690-108">hello telemetry from hello sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![Просмотр телеметрии устройства][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="bf690-110">Вызов метода на устройстве</span><span class="sxs-lookup"><span data-stu-id="bf690-110">Invoke a method on your device</span></span>
<span data-ttu-id="bf690-111">панель мониторинга Hello в решение для удаленного мониторинга hello включает методы tooinvoke на устройстве с помощью центра IoT.</span><span class="sxs-lookup"><span data-stu-id="bf690-111">hello dashboard in hello remote monitoring solution enables you tooinvoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="bf690-112">Например в hello удаленного решением для мониторинга, можно вызвать метод toosimulate, перезагрузка устройства.</span><span class="sxs-lookup"><span data-stu-id="bf690-112">For example, in hello remote monitoring solution you can invoke a method toosimulate rebooting a device.</span></span>

1. <span data-ttu-id="bf690-113">Hello удаленного мониторинга решения панели мониторинга щелкните **устройств** в hello левую панель toonavigate toohello **список устройств**.</span><span class="sxs-lookup"><span data-stu-id="bf690-113">In hello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="bf690-114">Нажмите кнопку **идентификатор устройства** для вашего устройства в hello **список устройств**.</span><span class="sxs-lookup"><span data-stu-id="bf690-114">Click **Device ID** for your device in hello **Devices list**.</span></span>
3. <span data-ttu-id="bf690-115">В hello **сведений об устройстве** нажмите кнопку **методы**.</span><span class="sxs-lookup"><span data-stu-id="bf690-115">In hello **Device details** panel, click **Methods**.</span></span>
   
    ![Методы устройства][13]
4. <span data-ttu-id="bf690-117">В hello **метод** раскрывающийся список, выберите **InitiateFirmwareUpdate**, а затем в **FWPACKAGEURI** введите пустой URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="bf690-117">In hello **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="bf690-118">Нажмите кнопку **вызвать метод** метод hello toocall на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="bf690-118">Click **Invoke Method** toocall hello method on hello device.</span></span>
   
    ![Вызов метода устройства][14]
   

5. <span data-ttu-id="bf690-120">Вы видите сообщение hello консоли устройства код запускается, когда устройство hello обрабатывает метод hello.</span><span class="sxs-lookup"><span data-stu-id="bf690-120">You see a message in hello console running your device code when hello device handles hello method.</span></span> <span data-ttu-id="bf690-121">результаты Hello hello метода добавляются toohello журнал hello решение портала:</span><span class="sxs-lookup"><span data-stu-id="bf690-121">hello results of hello method are added toohello history in hello solution portal:</span></span>

    ![Просмотр журнала методов][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="bf690-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bf690-123">Next steps</span></span>
<span data-ttu-id="bf690-124">статья Hello [Настройка предварительно настроенных решений] [ lnk-customize] описаны некоторые различия, можно расширить этот образец.</span><span class="sxs-lookup"><span data-stu-id="bf690-124">hello article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="bf690-125">В их число входит использование реальных датчиков и реализация дополнительных команд.</span><span class="sxs-lookup"><span data-stu-id="bf690-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="bf690-126">Дополнительные сведения о hello [разрешения на сайт hello azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="bf690-126">You can learn more about hello [permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
