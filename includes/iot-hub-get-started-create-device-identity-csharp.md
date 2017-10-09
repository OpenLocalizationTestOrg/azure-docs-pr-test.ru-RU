## <a name="create-a-device-identity"></a><span data-ttu-id="25f8b-101">Создание удостоверения устройства</span><span class="sxs-lookup"><span data-stu-id="25f8b-101">Create a device identity</span></span>
<span data-ttu-id="25f8b-102">В этом разделе создайте консольное приложение .NET, которое создает удостоверение устройства в реестре hello identity в вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="25f8b-102">In this section, you create a .NET console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="25f8b-103">Устройство не удается подключиться tooIoT концентратора, если оно не имеет запись в реестре удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="25f8b-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="25f8b-104">Дополнительные сведения см. в разделе hello раздел «Удостоверение реестра» hello [руководстве для разработчиков центра IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="25f8b-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="25f8b-105">При запуске это консольное приложение, он создает уникальный идентификатор устройства и ключ, что при отправке устройства в облако, устройство может использовать tooidentify самого сообщения tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="25f8b-105">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span> <span data-ttu-id="25f8b-106">Идентификаторы устройств чувствительны к регистру.</span><span class="sxs-lookup"><span data-stu-id="25f8b-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="25f8b-107">В Visual Studio добавьте новое решение tooa проекта Visual C# Windows классического с помощью hello **консольного приложения (.NET Framework)** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="25f8b-107">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="25f8b-108">Убедитесь, что hello версии платформы .NET Framework 4.5.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="25f8b-108">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="25f8b-109">Имя проекта hello **CreateDeviceIdentity** и имя решения hello **IoTHubGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="25f8b-109">Name hello project **CreateDeviceIdentity** and name hello solution **IoTHubGetStarted**.</span></span>
   
    ![Новый проект классического приложения Windows на языке Visual C#][10]
2. <span data-ttu-id="25f8b-111">В обозревателе решений щелкните правой кнопкой мыши hello **CreateDeviceIdentity** проекта, а затем нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="25f8b-111">In Solution Explorer, right-click hello **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="25f8b-112">В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **microsoft.azure.devices**выберите **установить** tooinstall Hello **Microsoft.Azure.Devices** пакета и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="25f8b-112">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="25f8b-113">Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="25f8b-113">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Окно "Диспетчер пакетов NuGet"][11]
4. <span data-ttu-id="25f8b-115">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="25f8b-115">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="25f8b-116">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="25f8b-116">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="25f8b-117">Замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="25f8b-117">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="25f8b-118">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="25f8b-118">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task AddDeviceAsync()
        {
            string deviceId = "myFirstDevice";
            Device device;
            try
            {
                device = await registryManager.AddDeviceAsync(new Device(deviceId));
            }
            catch (DeviceAlreadyExistsException)
            {
                device = await registryManager.GetDeviceAsync(deviceId);
            }
            Console.WriteLine("Generated device key: {0}", device.Authentication.SymmetricKey.PrimaryKey);
        }
   
    <span data-ttu-id="25f8b-119">Этот метод создает удостоверение устройства с идентификатором **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="25f8b-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="25f8b-120">(Если этот идентификатор устройства уже существует в реестре удостоверений hello, hello код просто извлекает hello существующих сведений об устройстве.) Затем приложение Hello отображает hello первичный ключ для этого удостоверения.</span><span class="sxs-lookup"><span data-stu-id="25f8b-120">(If that device ID already exists in hello identity registry, hello code simply retrieves hello existing device information.) hello app then displays hello primary key for that identity.</span></span> <span data-ttu-id="25f8b-121">Используйте этот ключ в центр IoT tooyour tooconnect приложения hello имитируемые устройства.</span><span class="sxs-lookup"><span data-stu-id="25f8b-121">You use this key in hello simulated device app tooconnect tooyour IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="25f8b-122">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="25f8b-122">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="25f8b-123">Запустите это приложение и запишите ключ устройства hello.</span><span class="sxs-lookup"><span data-stu-id="25f8b-123">Run this application, and make a note of hello device key.</span></span>
   
    ![Ключ устройства, созданном приложением hello][12]

> [!NOTE]
> <span data-ttu-id="25f8b-125">Hello реестра удостоверений центра IoT хранится только toohello устройства удостоверения tooenable безопасного доступа центра IoT.</span><span class="sxs-lookup"><span data-stu-id="25f8b-125">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="25f8b-126">Он сохраняет идентификаторы и ключи toouse устройства как учетные данные безопасности, а также включение или отключение флага, что toodisable доступа можно использовать для отдельных устройств.</span><span class="sxs-lookup"><span data-stu-id="25f8b-126">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="25f8b-127">Если приложению toostore другие метаданные для конкретного устройства, его следует использовать хранилище конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="25f8b-127">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="25f8b-128">Дополнительные сведения см. в [руководстве разработчика по Центру Интернета вещей][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="25f8b-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
