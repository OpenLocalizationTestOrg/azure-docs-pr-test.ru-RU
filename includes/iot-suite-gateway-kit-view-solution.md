## <a name="view-the-solution-dashboard"></a><span data-ttu-id="96aac-101">Просмотр панели мониторинга решения</span><span class="sxs-lookup"><span data-stu-id="96aac-101">View the solution dashboard</span></span>

<span data-ttu-id="96aac-102">Панель мониторинга решения позволяет управлять развернутым решением.</span><span class="sxs-lookup"><span data-stu-id="96aac-102">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="96aac-103">Например, можно просматривать данные телеметрии, добавлять устройства и вызывать методы.</span><span class="sxs-lookup"><span data-stu-id="96aac-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="96aac-104">Когда подготовка завершится и на плитке предварительно настроенного решения появится надпись **Готово**, нажмите кнопку **Запустить**. Панель мониторинга решения откроется в новой вкладке.</span><span class="sxs-lookup"><span data-stu-id="96aac-104">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![Запуск предварительно настроенного решения][img-launch-solution]

1. <span data-ttu-id="96aac-106">По умолчанию на портале решения отображается *панель мониторинга*.</span><span class="sxs-lookup"><span data-stu-id="96aac-106">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="96aac-107">Перейдите к другим областям портала решения с помощью меню в левой части страницы.</span><span class="sxs-lookup"><span data-stu-id="96aac-107">Navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Панель мониторинга предварительно настроенного решения для удаленного мониторинга][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="96aac-109">Добавление устройства</span><span class="sxs-lookup"><span data-stu-id="96aac-109">Add a device</span></span>

<span data-ttu-id="96aac-110">Чтобы устройство смогло подключиться к предварительно настроенному решению, оно должно пройти идентификацию в центре IoT с использованием допустимых учетных данных.</span><span class="sxs-lookup"><span data-stu-id="96aac-110">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="96aac-111">Учетные данные устройства можно получить на панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="96aac-111">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="96aac-112">Вы добавите их в клиентское приложение далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="96aac-112">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="96aac-113">Чтобы добавить устройство в решение для удаленного мониторинга, выполните следующие действия на панели мониторинга решения:</span><span class="sxs-lookup"><span data-stu-id="96aac-113">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="96aac-114">В левом нижнем углу панели мониторинга щелкните **Добавить устройство**.</span><span class="sxs-lookup"><span data-stu-id="96aac-114">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>

   ![Добавление устройства][1]

1. <span data-ttu-id="96aac-116">На панели **Пользовательское устройство** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="96aac-116">In the **Custom Device** panel, click **Add new**.</span></span>

   ![Добавление пользовательского устройства][2]

1. <span data-ttu-id="96aac-118">Установите переключатель **Позвольте мне определить собственный идентификатор устройства**.</span><span class="sxs-lookup"><span data-stu-id="96aac-118">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="96aac-119">Введите идентификатор устройства, например **device01**, и нажмите кнопку **Проверить идентификатор**, чтобы убедиться, что такое имя не используется в решении. Затем нажмите кнопку **Создать**, чтобы подготовить устройство.</span><span class="sxs-lookup"><span data-stu-id="96aac-119">Enter a Device ID such as **device01**, click **Check ID** to verify you haven't already used the name in your solution, and then click **Create** to provision the device.</span></span>

   ![Добавление идентификатора устройства][3]

1. <span data-ttu-id="96aac-121">Запишите учетные данные (**идентификатор устройства**, **имя узла в Центре Интернета вещей** и **ключ устройства**).</span><span class="sxs-lookup"><span data-stu-id="96aac-121">Make a note the device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="96aac-122">Эти значения потребуются клиентскому приложению на устройстве Intel NUC при подключении к решению для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="96aac-122">Your client application on the Intel NUC needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="96aac-123">Затем нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="96aac-123">Then click **Done**.</span></span>

    ![Просмотр учетных данных устройства][4]

1. <span data-ttu-id="96aac-125">Выберите устройство в списке устройств на панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="96aac-125">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="96aac-126">Затем на панели **Сведения об устройстве** щелкните **Включить устройство**.</span><span class="sxs-lookup"><span data-stu-id="96aac-126">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="96aac-127">Теперь текущее состояние устройства — **Работает**.</span><span class="sxs-lookup"><span data-stu-id="96aac-127">The status of your device is now **Running**.</span></span> <span data-ttu-id="96aac-128">Решение для удаленного мониторинга теперь может получать данные телеметрии с устройства и вызывать методы на устройстве.</span><span class="sxs-lookup"><span data-stu-id="96aac-128">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-launch-solution]: media/iot-suite-gateway-kit-view-solution/launch.png
[img-menu]: media/iot-suite-gateway-kit-view-solution/menu.png
[1]: media/iot-suite-gateway-kit-view-solution/suite0.png
[2]: media/iot-suite-gateway-kit-view-solution/suite1.png
[3]: media/iot-suite-gateway-kit-view-solution/suite2.png
[4]: media/iot-suite-gateway-kit-view-solution/suite3.png