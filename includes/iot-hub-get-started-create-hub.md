## <a name="create-an-iot-hub"></a><span data-ttu-id="c20db-101">Создание центра IoT</span><span class="sxs-lookup"><span data-stu-id="c20db-101">Create an IoT hub</span></span>
<span data-ttu-id="c20db-102">Создаете центр IoT для вашей tooconnect приложения имитированное устройство для.</span><span class="sxs-lookup"><span data-stu-id="c20db-102">Create an IoT hub for your simulated device app tooconnect to.</span></span> <span data-ttu-id="c20db-103">Hello следующие шаги показывают, как toocomplete это задач с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c20db-103">hello following steps show you how toocomplete this task by using hello Azure portal.</span></span>

1. <span data-ttu-id="c20db-104">Войдите в toohello [портал Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="c20db-104">Sign in toohello [Azure portal][lnk-portal].</span></span>
1. <span data-ttu-id="c20db-105">В hello Jumpbar щелкните **New** > **Интернета вещей** > **центр IoT**.</span><span class="sxs-lookup"><span data-stu-id="c20db-105">In hello Jumpbar, click **New** > **Internet of Things** > **IoT Hub**.</span></span>
   
    ![Навигационная панель портала Azure][1]
1. <span data-ttu-id="c20db-107">В hello **центр IoT** колонке выберите конфигурацию hello для вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="c20db-107">In hello **IoT hub** blade, choose hello configuration for your IoT hub.</span></span>
   
    ![Колонка "Центр Интернета вещей"][2]
   
   1. <span data-ttu-id="c20db-109">В hello **имя** введите имя для вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="c20db-109">In hello **Name** box, enter a name for your IoT hub.</span></span> <span data-ttu-id="c20db-110">Если hello **имя** действителен и доступных, отображается зеленая галочка в hello **имя** поле.</span><span class="sxs-lookup"><span data-stu-id="c20db-110">If hello **Name** is valid and available, a green check mark appears in hello **Name** box.</span></span>
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. <span data-ttu-id="c20db-111">Выберите [уровень цен и масштабирования][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="c20db-111">Select a [pricing and scale tier][lnk-pricing].</span></span> <span data-ttu-id="c20db-112">Для этого руководства задавать определенный уровень не нужно.</span><span class="sxs-lookup"><span data-stu-id="c20db-112">This tutorial does not require a specific tier.</span></span> <span data-ttu-id="c20db-113">В этом учебнике используется уровень free F1 hello.</span><span class="sxs-lookup"><span data-stu-id="c20db-113">For this tutorial, use hello free F1 tier.</span></span>
   1. <span data-ttu-id="c20db-114">В разделе **Группа ресурсов** создайте новую группу ресурсов или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="c20db-114">In **Resource group**, either create a resource group, or select an existing one.</span></span> <span data-ttu-id="c20db-115">Дополнительные сведения см. в разделе [с помощью ресурса группы toomanage ресурсам Azure][lnk-resource-groups].</span><span class="sxs-lookup"><span data-stu-id="c20db-115">For more information, see [Using resource groups toomanage your Azure resources][lnk-resource-groups].</span></span>
   1. <span data-ttu-id="c20db-116">В **расположение**, выберите hello toohost расположение вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="c20db-116">In **Location**, select hello location toohost your IoT hub.</span></span> <span data-ttu-id="c20db-117">В этом руководстве следует выбрать ближайшее к вам расположение.</span><span class="sxs-lookup"><span data-stu-id="c20db-117">For this tutorial, choose your nearest location.</span></span>
1. <span data-ttu-id="c20db-118">Выбрав параметры конфигурации центра IoT, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c20db-118">When you have chosen your IoT hub configuration options, click **Create**.</span></span>  <span data-ttu-id="c20db-119">Он может занять несколько минут для Azure toocreate концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="c20db-119">It can take a few minutes for Azure toocreate your IoT hub.</span></span> <span data-ttu-id="c20db-120">состояние toocheck hello, позволяющее наблюдать за hello на начальной панели hello или на панели уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="c20db-120">toocheck hello status, you can monitor hello progress on hello Startboard or in hello Notifications panel.</span></span>
   
    ![Состояние нового центра IoT][3]
1. <span data-ttu-id="c20db-122">При успешном создании центра IoT hello, щелкните hello новая Плитка для вашего центра IoT в колонке hello Azure портала tooopen hello hello новый центр IoT.</span><span class="sxs-lookup"><span data-stu-id="c20db-122">When hello IoT hub has been created successfully, click hello new tile for your IoT hub in hello Azure portal tooopen hello blade for hello new IoT hub.</span></span> <span data-ttu-id="c20db-123">Запишите hello **Hostname**, а затем нажмите кнопку **политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="c20db-123">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>
   
    ![Колонка нового центра IoT][4]
1. <span data-ttu-id="c20db-125">В hello **политики общего доступа** колонка, щелкните hello **iothubowner** политики, затем скопируйте и запишите hello строка подключения концентратора IoT hello **iothubowner** колонку.</span><span class="sxs-lookup"><span data-stu-id="c20db-125">In hello **Shared access policies** blade, click hello **iothubowner** policy, and then copy and make note of hello IoT Hub connection string in hello **iothubowner** blade.</span></span> <span data-ttu-id="c20db-126">Дополнительные сведения см. в разделе [управления доступом к] [ lnk-access-control] в hello «Центра IoT руководство разработчика».</span><span class="sxs-lookup"><span data-stu-id="c20db-126">For more information, see [Access control][lnk-access-control] in hello "IoT Hub developer guide."</span></span>
   
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
