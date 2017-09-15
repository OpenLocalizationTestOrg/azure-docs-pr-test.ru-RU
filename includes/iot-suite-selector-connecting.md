> [!div class="op_single_selector"]
> * [<span data-ttu-id="e644d-101">C в Windows</span><span class="sxs-lookup"><span data-stu-id="e644d-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="e644d-102">C в Linux</span><span class="sxs-lookup"><span data-stu-id="e644d-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="e644d-103">Node.js</span><span class="sxs-lookup"><span data-stu-id="e644d-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="e644d-104">Обзор сценария</span><span class="sxs-lookup"><span data-stu-id="e644d-104">Scenario overview</span></span>
<span data-ttu-id="e644d-105">В этом примере создается устройство, которое отправляет следующие данные телеметрии в [предварительно настроенное решение][lnk-what-are-preconfig-solutions] для удаленного мониторинга:</span><span class="sxs-lookup"><span data-stu-id="e644d-105">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="e644d-106">наружная температура;</span><span class="sxs-lookup"><span data-stu-id="e644d-106">External temperature</span></span>
* <span data-ttu-id="e644d-107">внутренняя температура;</span><span class="sxs-lookup"><span data-stu-id="e644d-107">Internal temperature</span></span>
* <span data-ttu-id="e644d-108">влажность.</span><span class="sxs-lookup"><span data-stu-id="e644d-108">Humidity</span></span>

<span data-ttu-id="e644d-109">В целях упрощения код на устройстве генерирует образцы значений, но мы рекомендуем расширить пример и подключить к устройству реальные датчики и отправить реальные данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="e644d-109">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span></span>

<span data-ttu-id="e644d-110">Устройство также может отвечать на методы, вызываемые из панели мониторинга решения, и значения требуемых свойств, заданные на панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="e644d-110">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span></span>

<span data-ttu-id="e644d-111">Для работы с этим руководством требуется активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="e644d-111">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="e644d-112">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e644d-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e644d-113">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="e644d-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e644d-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e644d-114">Before you start</span></span>
<span data-ttu-id="e644d-115">До написания кода для устройства необходимо подготовить свое предварительно настроенное решение для удаленного мониторинга, а затем подготовить в нем новое пользовательское устройство.</span><span class="sxs-lookup"><span data-stu-id="e644d-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="e644d-116">Подготовка предварительно настроенного решения для удаленного мониторинга</span><span class="sxs-lookup"><span data-stu-id="e644d-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="e644d-117">Созданное в этом руководстве устройство отправляет данные в экземпляр предварительно настроенного решения для [удаленного мониторинга][lnk-remote-monitoring].</span><span class="sxs-lookup"><span data-stu-id="e644d-117">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="e644d-118">Если вы еще не подготовили это решение в своей учетной записи Azure, то выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e644d-118">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span></span>

1. <span data-ttu-id="e644d-119">Чтобы создать решение, на странице <https://www.azureiotsuite.com/> щелкните знак **+**.</span><span class="sxs-lookup"><span data-stu-id="e644d-119">On the <https://www.azureiotsuite.com/> page, click **+** to create a solution.</span></span>
2. <span data-ttu-id="e644d-120">На панели **Удаленный мониторинг** щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e644d-120">Click **Select** on the **Remote monitoring** panel to create your solution.</span></span>
3. <span data-ttu-id="e644d-121">На странице **Create Remote monitoring solution** (Создание решения для удаленного мониторинга) введите **имя решения** по своему усмотрению, выберите **регион** для развертывания и подписку Azure, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="e644d-121">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span></span> <span data-ttu-id="e644d-122">Затем щелкните **Создать решение**.</span><span class="sxs-lookup"><span data-stu-id="e644d-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="e644d-123">Дождитесь завершения процесса подготовки.</span><span class="sxs-lookup"><span data-stu-id="e644d-123">Wait until the provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="e644d-124">В предварительно настроенных решениях используются платные службы Azure.</span><span class="sxs-lookup"><span data-stu-id="e644d-124">The preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="e644d-125">Закончив работу с предварительно настроенным решением, не забудьте удалить его из подписки, чтобы избежать ненужных расходов.</span><span class="sxs-lookup"><span data-stu-id="e644d-125">Be sure to remove the preconfigured solution from your subscription when you are done with it to avoid any unnecessary charges.</span></span> <span data-ttu-id="e644d-126">На странице <https://www.azureiotsuite.com/> можно полностью удалить предварительно настроенное решение из подписки.</span><span class="sxs-lookup"><span data-stu-id="e644d-126">You can completely remove a preconfigured solution from your subscription by visiting the <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="e644d-127">После завершения подготовки решения для удаленного мониторинга щелкните **Запустить** , чтобы открыть панель мониторинга этого решения в браузере.</span><span class="sxs-lookup"><span data-stu-id="e644d-127">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span></span>

![Панель мониторинга решения][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a><span data-ttu-id="e644d-129">Подготовка устройства в решении для удаленного мониторинга</span><span class="sxs-lookup"><span data-stu-id="e644d-129">Provision your device in the remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="e644d-130">Если вы уже подготовили устройство в решении, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="e644d-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="e644d-131">При создании клиентского приложения необходимо знать учетные данные устройства.</span><span class="sxs-lookup"><span data-stu-id="e644d-131">You need to know the device credentials when you create the client application.</span></span>
> 
> 

<span data-ttu-id="e644d-132">Чтобы устройство смогло подключиться к предварительно настроенному решению, оно должно пройти идентификацию в центре IoT с использованием допустимых учетных данных.</span><span class="sxs-lookup"><span data-stu-id="e644d-132">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="e644d-133">Учетные данные устройства можно получить на панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="e644d-133">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="e644d-134">Вы добавите их в клиентское приложение далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e644d-134">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="e644d-135">Чтобы добавить устройство в решение для удаленного мониторинга, выполните следующие действия на панели мониторинга решения:</span><span class="sxs-lookup"><span data-stu-id="e644d-135">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="e644d-136">В левом нижнем углу панели мониторинга щелкните **Добавить устройство**.</span><span class="sxs-lookup"><span data-stu-id="e644d-136">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>
   
   ![Добавление устройства][1]
2. <span data-ttu-id="e644d-138">На панели **Пользовательское устройство** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e644d-138">In the **Custom Device** panel, click **Add new**.</span></span>
   
   ![Добавление пользовательского устройства][2]
3. <span data-ttu-id="e644d-140">Установите переключатель **Позвольте мне определить собственный идентификатор устройства**.</span><span class="sxs-lookup"><span data-stu-id="e644d-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="e644d-141">Введите идентификатор устройства, например **mydevice**, и нажмите кнопку **Проверить идентификатор**, чтобы убедиться, что такое имя не используется. Затем нажмите кнопку **Создать**, чтобы подготовить устройство.</span><span class="sxs-lookup"><span data-stu-id="e644d-141">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span></span>
   
   ![Добавление идентификатора устройства][3]
4. <span data-ttu-id="e644d-143">Запишите учетные данные (идентификатор устройства, имя узла в Центре Интернета вещей и ключ устройства).</span><span class="sxs-lookup"><span data-stu-id="e644d-143">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="e644d-144">Эти значения потребуются клиентскому приложению при подключении к решению для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="e644d-144">Your client application needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="e644d-145">Затем нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="e644d-145">Then click **Done**.</span></span>
   
    ![Просмотр учетных данных устройства][4]
5. <span data-ttu-id="e644d-147">Выберите устройство в списке устройств на панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="e644d-147">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="e644d-148">Затем на панели **Сведения об устройстве** щелкните **Включить устройство**.</span><span class="sxs-lookup"><span data-stu-id="e644d-148">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="e644d-149">Теперь текущее состояние устройства — **Работает**.</span><span class="sxs-lookup"><span data-stu-id="e644d-149">The status of your device is now **Running**.</span></span> <span data-ttu-id="e644d-150">Решение для удаленного мониторинга теперь может получать данные телеметрии с устройства и вызывать методы на устройстве.</span><span class="sxs-lookup"><span data-stu-id="e644d-150">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/