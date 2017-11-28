## <a name="create-an-iot-hub"></a><span data-ttu-id="875ae-101">Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="875ae-101">Create an IoT hub</span></span>

1. <span data-ttu-id="875ae-102">На [портале Azure](https://portal.azure.com/) щелкните **Создать** > **Интернет вещей** > **Центр Интернета вещей**.</span><span class="sxs-lookup"><span data-stu-id="875ae-102">In the [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![Создание Центра Интернета вещей на портале Azure](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. <span data-ttu-id="875ae-104">В области **Центр Интернета вещей** введите следующие сведения для создания Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="875ae-104">In the **IoT hub** pane, enter the following information for your IoT hub:</span></span>

     <span data-ttu-id="875ae-105">**Имя.** Введите имя вашего центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="875ae-105">**Name**: Enter the name of your IoT hub.</span></span> <span data-ttu-id="875ae-106">Если введенное имя является допустимым, появится зеленая галочка.</span><span class="sxs-lookup"><span data-stu-id="875ae-106">If the name you enter is valid, a green check mark appears.</span></span>

     <span data-ttu-id="875ae-107">**Ценовая категория и категория масштабирования**. Выберите **бесплатную категорию F1**.</span><span class="sxs-lookup"><span data-stu-id="875ae-107">**Pricing and scale tier**: Select the **F1 - Free** tier.</span></span> <span data-ttu-id="875ae-108">Этот вариант подойдет для этой демонстрационной версии.</span><span class="sxs-lookup"><span data-stu-id="875ae-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="875ae-109">Дополнительные сведения о ценовых категориях и категориях масштабирования см. в [этой статье](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="875ae-109">For more information, see the [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

     <span data-ttu-id="875ae-110">**Группа ресурсов**. Создайте группу ресурсов для размещения Центра Интернета вещей или используйте имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="875ae-110">**Resource group**: Create a resource group to host the IoT hub or use an existing one.</span></span> <span data-ttu-id="875ae-111">Дополнительные сведения см. в статье [Управление ресурсами Azure через портал](../articles/azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="875ae-111">For more information, see [Use resource groups to manage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

     <span data-ttu-id="875ae-112">**Расположение**. Выберите расположение, ближайшее к созданному Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="875ae-112">**Location**: Select the closest location to you where the IoT hub is created.</span></span>

     <span data-ttu-id="875ae-113">**Закрепить на панели мониторинга.** Установите этот флажок, чтобы быстро открывать Центр Интернета вещей с помощью панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="875ae-113">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Ввод информации для создания Центра Интернета вещей](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. <span data-ttu-id="875ae-115">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="875ae-115">Click **Create**.</span></span> <span data-ttu-id="875ae-116">Создание Центра Интернета вещей может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="875ae-116">Your IoT hub might take a few minutes to create.</span></span> <span data-ttu-id="875ae-117">Ход создания отображается на панели **уведомлений**.</span><span class="sxs-lookup"><span data-stu-id="875ae-117">You can see progress in the **Notifications** pane.</span></span>

   ![Просмотр уведомлений о ходе создания Центра Интернета вещей](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. <span data-ttu-id="875ae-119">После создания Центра Интернета вещей щелкните его на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="875ae-119">After your IoT hub is created, click it on the dashboard.</span></span> <span data-ttu-id="875ae-120">Запишите **имя узла**, а затем щелкните **Политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="875ae-120">Make a note of the **Hostname**, and then click **Shared access policies**.</span></span>

   ![Получение имени узла для Центра Интернета вещей](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. <span data-ttu-id="875ae-122">В области **Политики общего доступа** выберите политику **iothubowner**, а затем скопируйте и запишите **строку подключения** Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="875ae-122">In the **Shared access policies** pane, click the **iothubowner** policy, and then copy and make a note of the **Connection string** of your IoT hub.</span></span> <span data-ttu-id="875ae-123">Дополнительные сведения см. в статье [Управление доступом к Центру Интернета вещей](../articles/iot-hub/iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="875ae-123">For more information, see [Control access to IoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

> [!NOTE] 
<span data-ttu-id="875ae-124">Строка подключения iothubowner в этом руководстве по установке не понадобится.</span><span class="sxs-lookup"><span data-stu-id="875ae-124">You will not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="875ae-125">Однако она может понадобиться для некоторых руководств по различным сценариям Интернета вещей после завершения этой установки.</span><span class="sxs-lookup"><span data-stu-id="875ae-125">However, you may need it for some of the tutorials on different IoT scenarios after you complete this set-up.</span></span>

   ![Получение строки подключения Центра Интернета вещей](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-the-iot-hub-for-your-device"></a><span data-ttu-id="875ae-127">Регистрация устройства в Центре Интернета вещей ваших устройств</span><span class="sxs-lookup"><span data-stu-id="875ae-127">Register a device in the IoT hub for your device</span></span>

1. <span data-ttu-id="875ae-128">Откройте Центр Интернета вещей на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="875ae-128">In the [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>

2. <span data-ttu-id="875ae-129">Щелкните **Обозреватель устройств**.</span><span class="sxs-lookup"><span data-stu-id="875ae-129">Click **Device Explorer**.</span></span>
3. <span data-ttu-id="875ae-130">На панели обозревателя устройства щелкните **Добавить** для добавления устройства в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="875ae-130">In the Device Explorer pane, click **Add** to add a device to your IoT hub.</span></span> <span data-ttu-id="875ae-131">После этого выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="875ae-131">Then do the following:</span></span>

   <span data-ttu-id="875ae-132">**Идентификатор устройства.** Введите идентификатор нового устройства.</span><span class="sxs-lookup"><span data-stu-id="875ae-132">**Device ID**: Enter the ID of the new device.</span></span> <span data-ttu-id="875ae-133">Идентификаторы устройств чувствительны к регистру.</span><span class="sxs-lookup"><span data-stu-id="875ae-133">Device IDs are case sensitive.</span></span>

   <span data-ttu-id="875ae-134">**Тип проверки подлинности.** Выберите **Симметричный ключ**.</span><span class="sxs-lookup"><span data-stu-id="875ae-134">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="875ae-135">**Auto Generate Keys** (Автоматическое создание ключей). Установите флажок.</span><span class="sxs-lookup"><span data-stu-id="875ae-135">**Auto Generate Keys**: Select this check box.</span></span>

   <span data-ttu-id="875ae-136">**Подключить устройство к центру IoT**. Щелкните **Включить**.</span><span class="sxs-lookup"><span data-stu-id="875ae-136">**Connect device to IoT Hub**: Click **Enable**.</span></span>

   ![Добавление устройства в Device Explorer Центра Интернета вещей](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. <span data-ttu-id="875ae-138">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="875ae-138">Click **Save**.</span></span>
5. <span data-ttu-id="875ae-139">Создав устройство, откройте его в области **Обозреватель устройств**.</span><span class="sxs-lookup"><span data-stu-id="875ae-139">After the device is created, open the device in the **Device Explorer** pane.</span></span>
6. <span data-ttu-id="875ae-140">Запишите первичный ключ строки подключения.</span><span class="sxs-lookup"><span data-stu-id="875ae-140">Make a note of the primary key of the connection string.</span></span>

   ![Получение строки подключения устройства](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
