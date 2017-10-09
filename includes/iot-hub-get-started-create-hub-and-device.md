## <a name="create-an-iot-hub"></a><span data-ttu-id="cbc13-101">Создание центра IoT</span><span class="sxs-lookup"><span data-stu-id="cbc13-101">Create an IoT hub</span></span>

1. <span data-ttu-id="cbc13-102">В hello [портал Azure](https://portal.azure.com/), нажмите кнопку **New** > **Интернета вещей** > **центр IoT**.</span><span class="sxs-lookup"><span data-stu-id="cbc13-102">In hello [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![Создать центр IoT в hello портал Azure](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. <span data-ttu-id="cbc13-104">В hello **центр IoT** области введите следующие сведения для вашего центра IoT hello:</span><span class="sxs-lookup"><span data-stu-id="cbc13-104">In hello **IoT hub** pane, enter hello following information for your IoT hub:</span></span>

     <span data-ttu-id="cbc13-105">**Имя**: Введите имя вашего центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="cbc13-105">**Name**: Enter hello name of your IoT hub.</span></span> <span data-ttu-id="cbc13-106">Если вы вводите имя hello допустим, отображается зеленая галочка.</span><span class="sxs-lookup"><span data-stu-id="cbc13-106">If hello name you enter is valid, a green check mark appears.</span></span>

     <span data-ttu-id="cbc13-107">**Ценах и масштабировании уровня**: выберите hello **F1 - свободного** уровня.</span><span class="sxs-lookup"><span data-stu-id="cbc13-107">**Pricing and scale tier**: Select hello **F1 - Free** tier.</span></span> <span data-ttu-id="cbc13-108">Этот вариант подойдет для этой демонстрационной версии.</span><span class="sxs-lookup"><span data-stu-id="cbc13-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="cbc13-109">Дополнительные сведения см. в разделе hello [Ценовая категория и категория масштабирования](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="cbc13-109">For more information, see hello [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

     <span data-ttu-id="cbc13-110">**Группа ресурсов**: создание концентратора IoT hello toohost группы ресурсов или используйте существующую.</span><span class="sxs-lookup"><span data-stu-id="cbc13-110">**Resource group**: Create a resource group toohost hello IoT hub or use an existing one.</span></span> <span data-ttu-id="cbc13-111">Дополнительные сведения см. в разделе [toomanage группы на использование ресурсов, ресурсов Azure](../articles/azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cbc13-111">For more information, see [Use resource groups toomanage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

     <span data-ttu-id="cbc13-112">**Расположение**: выберите hello ближайший tooyou расположение, где создается центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="cbc13-112">**Location**: Select hello closest location tooyou where hello IoT hub is created.</span></span>

     <span data-ttu-id="cbc13-113">**ПИН-код toodashboard**: выберите этот параметр для облегчения доступа центра IoT tooyour из панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="cbc13-113">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Введите сведения toocreate ваш центр IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. <span data-ttu-id="cbc13-115">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="cbc13-115">Click **Create**.</span></span> <span data-ttu-id="cbc13-116">Концентратор IoT может занять несколько минут toocreate.</span><span class="sxs-lookup"><span data-stu-id="cbc13-116">Your IoT hub might take a few minutes toocreate.</span></span> <span data-ttu-id="cbc13-117">Вы увидите ход выполнения в hello **уведомления** области.</span><span class="sxs-lookup"><span data-stu-id="cbc13-117">You can see progress in hello **Notifications** pane.</span></span>

   ![Просмотр уведомлений о ходе создания Центра Интернета вещей](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. <span data-ttu-id="cbc13-119">После создания вашего центра IoT, щелкните его на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="cbc13-119">After your IoT hub is created, click it on hello dashboard.</span></span> <span data-ttu-id="cbc13-120">Запишите hello **Hostname**, а затем нажмите кнопку **политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="cbc13-120">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>

   ![Получение имени узла hello из вашего центра IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. <span data-ttu-id="cbc13-122">В hello **политики общего доступа** панели щелкните hello **iothubowner** политики и затем копировать и запишите hello **строка подключения** из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="cbc13-122">In hello **Shared access policies** pane, click hello **iothubowner** policy, and then copy and make a note of hello **Connection string** of your IoT hub.</span></span> <span data-ttu-id="cbc13-123">Дополнительные сведения см. в разделе [tooIoT управления доступом концентратора](../articles/iot-hub/iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="cbc13-123">For more information, see [Control access tooIoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

> [!NOTE] 
<span data-ttu-id="cbc13-124">Строка подключения iothubowner в этом руководстве по установке не понадобится.</span><span class="sxs-lookup"><span data-stu-id="cbc13-124">You will not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="cbc13-125">Тем не менее может потребоваться его для некоторых учебников hello в различных сценариях IoT после завершения этой установки.</span><span class="sxs-lookup"><span data-stu-id="cbc13-125">However, you may need it for some of hello tutorials on different IoT scenarios after you complete this set-up.</span></span>

   ![Получение строки подключения Центра Интернета вещей](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a><span data-ttu-id="cbc13-127">Регистрация устройства в центр IoT hello для устройства</span><span class="sxs-lookup"><span data-stu-id="cbc13-127">Register a device in hello IoT hub for your device</span></span>

1. <span data-ttu-id="cbc13-128">В hello [портал Azure](https://portal.azure.com/), откройте ваш центр IoT.</span><span class="sxs-lookup"><span data-stu-id="cbc13-128">In hello [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>

2. <span data-ttu-id="cbc13-129">Щелкните **Обозреватель устройств**.</span><span class="sxs-lookup"><span data-stu-id="cbc13-129">Click **Device Explorer**.</span></span>
3. <span data-ttu-id="cbc13-130">В панели проводника устройства hello, щелкните **добавить** tooadd концентратор IoT tooyour устройства.</span><span class="sxs-lookup"><span data-stu-id="cbc13-130">In hello Device Explorer pane, click **Add** tooadd a device tooyour IoT hub.</span></span> <span data-ttu-id="cbc13-131">Затем hello следующие:</span><span class="sxs-lookup"><span data-stu-id="cbc13-131">Then do hello following:</span></span>

   <span data-ttu-id="cbc13-132">**Идентификатор устройства**: Введите идентификатор hello hello новое устройство.</span><span class="sxs-lookup"><span data-stu-id="cbc13-132">**Device ID**: Enter hello ID of hello new device.</span></span> <span data-ttu-id="cbc13-133">Идентификаторы устройств чувствительны к регистру.</span><span class="sxs-lookup"><span data-stu-id="cbc13-133">Device IDs are case sensitive.</span></span>

   <span data-ttu-id="cbc13-134">**Тип проверки подлинности.** Выберите **Симметричный ключ**.</span><span class="sxs-lookup"><span data-stu-id="cbc13-134">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="cbc13-135">**Auto Generate Keys** (Автоматическое создание ключей). Установите флажок.</span><span class="sxs-lookup"><span data-stu-id="cbc13-135">**Auto Generate Keys**: Select this check box.</span></span>

   <span data-ttu-id="cbc13-136">**Подключение устройства tooIoT концентратора**: щелкните **включить**.</span><span class="sxs-lookup"><span data-stu-id="cbc13-136">**Connect device tooIoT Hub**: Click **Enable**.</span></span>

   ![Добавление устройства в hello обозреватель устройств из вашего центра IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. <span data-ttu-id="cbc13-138">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cbc13-138">Click **Save**.</span></span>
5. <span data-ttu-id="cbc13-139">После создания устройства Привет открыть устройство hello в hello **обозреватель устройств** области.</span><span class="sxs-lookup"><span data-stu-id="cbc13-139">After hello device is created, open hello device in hello **Device Explorer** pane.</span></span>
6. <span data-ttu-id="cbc13-140">Запишите первичный ключ hello hello строки соединения.</span><span class="sxs-lookup"><span data-stu-id="cbc13-140">Make a note of hello primary key of hello connection string.</span></span>

   ![Получить строку подключения устройства hello](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
