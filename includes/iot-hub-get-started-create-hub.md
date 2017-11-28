## <a name="create-an-iot-hub"></a><span data-ttu-id="b7613-101">Создание центра IoT</span><span class="sxs-lookup"><span data-stu-id="b7613-101">Create an IoT hub</span></span>
<span data-ttu-id="b7613-102">Создайте центр Интернета вещей, к которому будет подключено приложение, имитирующее устройство.</span><span class="sxs-lookup"><span data-stu-id="b7613-102">Create an IoT hub for your simulated device app to connect to.</span></span> <span data-ttu-id="b7613-103">Ниже показано, как это сделать с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="b7613-103">The following steps show you how to complete this task by using the Azure portal.</span></span>

1. <span data-ttu-id="b7613-104">Войдите на [портал Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="b7613-104">Sign in to the [Azure portal][lnk-portal].</span></span>
1. <span data-ttu-id="b7613-105">На навигационной панели щелкните **Создать** > **Интернет вещей** > **Центр Интернета вещей**.</span><span class="sxs-lookup"><span data-stu-id="b7613-105">In the Jumpbar, click **New** > **Internet of Things** > **IoT Hub**.</span></span>
   
    ![Навигационная панель портала Azure][1]
1. <span data-ttu-id="b7613-107">В колонке **Центр IoT** выберите конфигурацию для центра IoT.</span><span class="sxs-lookup"><span data-stu-id="b7613-107">In the **IoT hub** blade, choose the configuration for your IoT hub.</span></span>
   
    ![Колонка "Центр IoT"][2]
   
   1. <span data-ttu-id="b7613-109">В поле **Имя** введите имя центра IoT.</span><span class="sxs-lookup"><span data-stu-id="b7613-109">In the **Name** box, enter a name for your IoT hub.</span></span> <span data-ttu-id="b7613-110">После проверки **имени** рядом с полем **Имя** появится зеленая галочка.</span><span class="sxs-lookup"><span data-stu-id="b7613-110">If the **Name** is valid and available, a green check mark appears in the **Name** box.</span></span>
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. <span data-ttu-id="b7613-111">Выберите [уровень цен и масштабирования][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="b7613-111">Select a [pricing and scale tier][lnk-pricing].</span></span> <span data-ttu-id="b7613-112">Для этого руководства задавать определенный уровень не нужно.</span><span class="sxs-lookup"><span data-stu-id="b7613-112">This tutorial does not require a specific tier.</span></span> <span data-ttu-id="b7613-113">В этом руководстве используется уровень F1 (бесплатный).</span><span class="sxs-lookup"><span data-stu-id="b7613-113">For this tutorial, use the free F1 tier.</span></span>
   1. <span data-ttu-id="b7613-114">В разделе **Группа ресурсов** создайте новую группу ресурсов или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="b7613-114">In **Resource group**, either create a resource group, or select an existing one.</span></span> <span data-ttu-id="b7613-115">Дополнительные сведения см. в статье [Управление ресурсами Azure через портал][lnk-resource-groups].</span><span class="sxs-lookup"><span data-stu-id="b7613-115">For more information, see [Using resource groups to manage your Azure resources][lnk-resource-groups].</span></span>
   1. <span data-ttu-id="b7613-116">**Расположение**— выберите расположение для размещения центра IoT.</span><span class="sxs-lookup"><span data-stu-id="b7613-116">In **Location**, select the location to host your IoT hub.</span></span> <span data-ttu-id="b7613-117">В этом руководстве следует выбрать ближайшее к вам расположение.</span><span class="sxs-lookup"><span data-stu-id="b7613-117">For this tutorial, choose your nearest location.</span></span>
1. <span data-ttu-id="b7613-118">Выбрав параметры конфигурации центра IoT, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b7613-118">When you have chosen your IoT hub configuration options, click **Create**.</span></span>  <span data-ttu-id="b7613-119">Создание центра IoT может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="b7613-119">It can take a few minutes for Azure to create your IoT hub.</span></span> <span data-ttu-id="b7613-120">Чтобы проверить состояние, следите за ходом выполнения на начальной панели или панели уведомлений.</span><span class="sxs-lookup"><span data-stu-id="b7613-120">To check the status, you can monitor the progress on the Startboard or in the Notifications panel.</span></span>
   
    ![Состояние нового центра IoT][3]
1. <span data-ttu-id="b7613-122">Когда Центр Интернета вещей будет создан, щелкните на портале Azure новую плитку для центра, чтобы открыть соответствующую колонку.</span><span class="sxs-lookup"><span data-stu-id="b7613-122">When the IoT hub has been created successfully, click the new tile for your IoT hub in the Azure portal to open the blade for the new IoT hub.</span></span> <span data-ttu-id="b7613-123">Запишите **имя узла**, а затем щелкните **Политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="b7613-123">Make a note of the **Hostname**, and then click **Shared access policies**.</span></span>
   
    ![Колонка нового центра IoT][4]
1. <span data-ttu-id="b7613-125">В колонке **Политики общего доступа** выберите политику **iothubowner**, а затем скопируйте и запишите строку подключения в колонке **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="b7613-125">In the **Shared access policies** blade, click the **iothubowner** policy, and then copy and make note of the IoT Hub connection string in the **iothubowner** blade.</span></span> <span data-ttu-id="b7613-126">Дополнительные сведения см. в разделе [Контроль доступа][lnk-access-control] в руководстве для разработчиков Центра Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="b7613-126">For more information, see [Access control][lnk-access-control] in the "IoT Hub developer guide."</span></span>
   
    ![Колонка "Политики общего доступа"][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
