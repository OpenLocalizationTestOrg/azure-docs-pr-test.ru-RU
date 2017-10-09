> [!div class="op_single_selector"]
> * [<span data-ttu-id="716d8-101">C в Windows</span><span class="sxs-lookup"><span data-stu-id="716d8-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="716d8-102">C в Linux</span><span class="sxs-lookup"><span data-stu-id="716d8-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="716d8-103">Node.js</span><span class="sxs-lookup"><span data-stu-id="716d8-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="716d8-104">Обзор сценария</span><span class="sxs-lookup"><span data-stu-id="716d8-104">Scenario overview</span></span>
<span data-ttu-id="716d8-105">В этом случае создайте устройство, которое отправляет hello следующие удаленный мониторинг телеметрии toohello [предварительно настроенное решение][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="716d8-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="716d8-106">наружная температура;</span><span class="sxs-lookup"><span data-stu-id="716d8-106">External temperature</span></span>
* <span data-ttu-id="716d8-107">внутренняя температура;</span><span class="sxs-lookup"><span data-stu-id="716d8-107">Internal temperature</span></span>
* <span data-ttu-id="716d8-108">влажность.</span><span class="sxs-lookup"><span data-stu-id="716d8-108">Humidity</span></span>

<span data-ttu-id="716d8-109">Для простоты кода hello на устройстве hello приводит к возникновению ошибки образцы значений, но мы рекомендуем вам tooextend hello образец подключение устройства tooyour реальные датчиков и отправки реальные данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="716d8-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="716d8-110">Hello устройство будет также может toorespond toomethods из панели мониторинга решения hello и требуемого значения свойств, заданные в панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="716d8-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="716d8-111">toocomplete этого учебника требуется активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="716d8-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="716d8-112">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="716d8-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="716d8-113">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="716d8-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="716d8-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="716d8-114">Before you start</span></span>
<span data-ttu-id="716d8-115">До написания кода для устройства необходимо подготовить свое предварительно настроенное решение для удаленного мониторинга, а затем подготовить в нем новое пользовательское устройство.</span><span class="sxs-lookup"><span data-stu-id="716d8-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="716d8-116">Подготовка предварительно настроенного решения для удаленного мониторинга</span><span class="sxs-lookup"><span data-stu-id="716d8-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="716d8-117">устройство Hello, создан в этом учебнике отправляет экземпляра tooan данных hello [удаленный мониторинг] [ lnk-remote-monitoring] предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="716d8-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="716d8-118">Если это еще не было предоставлено hello удаленное наблюдение предварительно настроенных решений в вашей учетной записью Azure, используйте hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="716d8-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="716d8-119">На hello <https://www.azureiotsuite.com/> щелкните  **+**  toocreate решения.</span><span class="sxs-lookup"><span data-stu-id="716d8-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="716d8-120">Нажмите кнопку **выберите** на hello **удаленный мониторинг** панели toocreate решения.</span><span class="sxs-lookup"><span data-stu-id="716d8-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="716d8-121">На hello **создания удаленного решением для мониторинга** введите **имя решения** по своему усмотрению выберите hello **область** toodeploy для и выберите hello Azure toouse toowant подписки.</span><span class="sxs-lookup"><span data-stu-id="716d8-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="716d8-122">Затем щелкните **Создать решение**.</span><span class="sxs-lookup"><span data-stu-id="716d8-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="716d8-123">Дождитесь завершения процесса подготовки hello.</span><span class="sxs-lookup"><span data-stu-id="716d8-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="716d8-124">предварительно настроенное Hello решения используют оплаты служб Azure.</span><span class="sxs-lookup"><span data-stu-id="716d8-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="716d8-125">Убедитесь, что tooremove hello предварительно настроенных решений из подписки, когда вы завершили работу с ним tooavoid все ненужные расходы.</span><span class="sxs-lookup"><span data-stu-id="716d8-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="716d8-126">Можно полностью удалить предварительно настроенных решений из подписки, перейдя по адресу hello <https://www.azureiotsuite.com/> страницы.</span><span class="sxs-lookup"><span data-stu-id="716d8-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="716d8-127">После завершения процесса для hello удаленного решением для мониторинга инициализации hello, нажмите кнопку **запуска** tooopen hello решения и панели мониторинга в браузере.</span><span class="sxs-lookup"><span data-stu-id="716d8-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Панель мониторинга решения][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="716d8-129">Подготовка устройства в hello удаленного решением для мониторинга</span><span class="sxs-lookup"><span data-stu-id="716d8-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="716d8-130">Если вы уже подготовили устройство в решении, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="716d8-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="716d8-131">Необходимы учетные данные устройства hello tooknow, при создании клиентского приложения hello.</span><span class="sxs-lookup"><span data-stu-id="716d8-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="716d8-132">Для решения tooconnect toohello предварительно настроенных устройств, он должен идентифицировать себя tooIoT концентратора используя действительные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="716d8-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="716d8-133">Учетные данные устройства hello можно извлечь из панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="716d8-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="716d8-134">Включать учетные данные устройства hello в клиентском приложении, далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="716d8-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="716d8-135">tooadd tooyour удаленного мониторинга устройствами завершения hello следующие шаги на панели мониторинга hello решения:</span><span class="sxs-lookup"><span data-stu-id="716d8-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="716d8-136">В hello левом нижнем углу панели мониторинга hello, щелкните **добавить устройство**.</span><span class="sxs-lookup"><span data-stu-id="716d8-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Добавление устройства][1]
2. <span data-ttu-id="716d8-138">В hello **пользовательских устройств** нажмите кнопку **добавить новую**.</span><span class="sxs-lookup"><span data-stu-id="716d8-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Добавление пользовательского устройства][2]
3. <span data-ttu-id="716d8-140">Установите переключатель **Позвольте мне определить собственный идентификатор устройства**.</span><span class="sxs-lookup"><span data-stu-id="716d8-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="716d8-141">Введите идентификатор устройства, например **mydevice**, нажмите кнопку **проверить идентификатор** tooverify таким именем еще не используется и нажмите кнопку **создать** tooprovision hello устройства.</span><span class="sxs-lookup"><span data-stu-id="716d8-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Добавление идентификатора устройства][3]
4. <span data-ttu-id="716d8-143">Перевести устройство hello Примечание учетные данные (идентификатор устройства, имя узла концентратора IoT и ключ устройства).</span><span class="sxs-lookup"><span data-stu-id="716d8-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="716d8-144">Клиент приложению эти значения tooconnect toohello удаленного решением для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="716d8-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="716d8-145">Затем нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="716d8-145">Then click **Done**.</span></span>
   
    ![Просмотр учетных данных устройства][4]
5. <span data-ttu-id="716d8-147">Выберите устройство в списке устройств hello в панель мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="716d8-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="716d8-148">Затем в hello **сведений об устройстве** нажмите кнопку **включить устройство**.</span><span class="sxs-lookup"><span data-stu-id="716d8-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="716d8-149">Теперь задано состояние Hello устройства **под управлением**.</span><span class="sxs-lookup"><span data-stu-id="716d8-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="716d8-150">решение для удаленного мониторинга Hello теперь можно получать данные телеметрии с устройства и вызова методов на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="716d8-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/