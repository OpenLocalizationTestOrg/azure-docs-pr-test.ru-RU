## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="4396f-101">Представление hello решений мониторинга</span><span class="sxs-lookup"><span data-stu-id="4396f-101">View hello solution dashboard</span></span>

<span data-ttu-id="4396f-102">панель мониторинга Hello решение позволяет toomanage hello развертывания решения.</span><span class="sxs-lookup"><span data-stu-id="4396f-102">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="4396f-103">Например, можно просматривать данные телеметрии, добавлять устройства и вызывать методы.</span><span class="sxs-lookup"><span data-stu-id="4396f-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="4396f-104">После подготовки hello завершения и указывает hello плитки для предварительно настроенного решения **готовности**, выберите **запуска** tooopen на новой вкладке портал удаленного мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="4396f-104">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Запустите hello предварительно настроенных решений][img-launch-solution]

1. <span data-ttu-id="4396f-106">По умолчанию hello решение портала отображает hello *мониторинга*.</span><span class="sxs-lookup"><span data-stu-id="4396f-106">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="4396f-107">Перейдите tooother области портала hello решения, с помощью меню hello hello левой стороны страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="4396f-107">Navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Панель мониторинга предварительно настроенного решения для удаленного мониторинга][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="4396f-109">Добавление устройства</span><span class="sxs-lookup"><span data-stu-id="4396f-109">Add a device</span></span>

<span data-ttu-id="4396f-110">Для решения tooconnect toohello предварительно настроенных устройств, он должен идентифицировать себя tooIoT концентратора используя действительные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="4396f-110">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="4396f-111">Учетные данные устройства hello можно извлечь из панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="4396f-111">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="4396f-112">Включать учетные данные устройства hello в клиентском приложении, далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="4396f-112">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="4396f-113">tooadd tooyour удаленного мониторинга устройствами завершения hello следующие шаги на панели мониторинга hello решения:</span><span class="sxs-lookup"><span data-stu-id="4396f-113">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="4396f-114">В hello левом нижнем углу панели мониторинга hello, щелкните **добавить устройство**.</span><span class="sxs-lookup"><span data-stu-id="4396f-114">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>

   ![Добавление устройства][1]

1. <span data-ttu-id="4396f-116">В hello **пользовательских устройств** нажмите кнопку **добавить новую**.</span><span class="sxs-lookup"><span data-stu-id="4396f-116">In hello **Custom Device** panel, click **Add new**.</span></span>

   ![Добавление пользовательского устройства][2]

1. <span data-ttu-id="4396f-118">Установите переключатель **Позвольте мне определить собственный идентификатор устройства**.</span><span class="sxs-lookup"><span data-stu-id="4396f-118">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="4396f-119">Введите идентификатор устройства, например **device01**, нажмите кнопку **проверить идентификатор** tooverify еще не использовалась hello имя решения и нажмите кнопку **создать** tooprovision hello устройства.</span><span class="sxs-lookup"><span data-stu-id="4396f-119">Enter a Device ID such as **device01**, click **Check ID** tooverify you haven't already used hello name in your solution, and then click **Create** tooprovision hello device.</span></span>

   ![Добавление идентификатора устройства][3]

1. <span data-ttu-id="4396f-121">Сделать устройство hello Примечание учетные данные (**идентификатор устройства**, **имя узла концентратора IoT**, и **ключ устройства**).</span><span class="sxs-lookup"><span data-stu-id="4396f-121">Make a note hello device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="4396f-122">Клиентское приложение на hello Intel NUC должен toohello tooconnect эти значения удаленного решением для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="4396f-122">Your client application on hello Intel NUC needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="4396f-123">Затем нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="4396f-123">Then click **Done**.</span></span>

    ![Просмотр учетных данных устройства][4]

1. <span data-ttu-id="4396f-125">Выберите устройство в списке устройств hello в панель мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="4396f-125">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="4396f-126">Затем в hello **сведений об устройстве** нажмите кнопку **включить устройство**.</span><span class="sxs-lookup"><span data-stu-id="4396f-126">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="4396f-127">Теперь задано состояние Hello устройства **под управлением**.</span><span class="sxs-lookup"><span data-stu-id="4396f-127">hello status of your device is now **Running**.</span></span> <span data-ttu-id="4396f-128">решение для удаленного мониторинга Hello теперь можно получать данные телеметрии с устройства и вызова методов на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="4396f-128">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-launch-solution]: media/iot-suite-gateway-kit-view-solution/launch.png
[img-menu]: media/iot-suite-gateway-kit-view-solution/menu.png
[1]: media/iot-suite-gateway-kit-view-solution/suite0.png
[2]: media/iot-suite-gateway-kit-view-solution/suite1.png
[3]: media/iot-suite-gateway-kit-view-solution/suite2.png
[4]: media/iot-suite-gateway-kit-view-solution/suite3.png