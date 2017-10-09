## <a name="create-a-device-identity"></a>Создание удостоверения устройства
В этом разделе создайте консольное приложение .NET, которое создает удостоверение устройства в реестре hello identity в вашего центра IoT. Устройство не удается подключиться tooIoT концентратора, если оно не имеет запись в реестре удостоверений hello. Дополнительные сведения см. в разделе hello раздел «Удостоверение реестра» hello [руководстве для разработчиков центра IoT][lnk-devguide-identity]. При запуске это консольное приложение, он создает уникальный идентификатор устройства и ключ, что при отправке устройства в облако, устройство может использовать tooidentify самого сообщения tooIoT концентратора. Идентификаторы устройств чувствительны к регистру.

1. В Visual Studio добавьте новое решение tooa проекта Visual C# Windows классического с помощью hello **консольного приложения (.NET Framework)** шаблона проекта. Убедитесь, что hello версии платформы .NET Framework 4.5.1 или более поздней версии. Имя проекта hello **CreateDeviceIdentity** и имя решения hello **IoTHubGetStarted**.
   
    ![Новый проект классического приложения Windows на языке Visual C#][10]
2. В обозревателе решений щелкните правой кнопкой мыши hello **CreateDeviceIdentity** проекта, а затем нажмите кнопку **управление пакетами NuGet**.
3. В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **microsoft.azure.devices**выберите **установить** tooinstall Hello **Microsoft.Azure.Devices** пакета и примите условия использования hello. Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.
   
    ![Окно "Диспетчер пакетов NuGet"][11]
4. Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. Добавьте следующие поля toohello hello **программы** класса. Замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. Добавьте следующий метод toohello hello **программы** класса:
   
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
   
    Этот метод создает удостоверение устройства с идентификатором **myFirstDevice**. (Если этот идентификатор устройства уже существует в реестре удостоверений hello, hello код просто извлекает hello существующих сведений об устройстве.) Затем приложение Hello отображает hello первичный ключ для этого удостоверения. Используйте этот ключ в центр IoT tooyour tooconnect приложения hello имитируемые устройства.
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. Наконец, добавьте следующие строки toohello hello **Main** метод:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. Запустите это приложение и запишите ключ устройства hello.
   
    ![Ключ устройства, созданном приложением hello][12]

> [!NOTE]
> Hello реестра удостоверений центра IoT хранится только toohello устройства удостоверения tooenable безопасного доступа центра IoT. Он сохраняет идентификаторы и ключи toouse устройства как учетные данные безопасности, а также включение или отключение флага, что toodisable доступа можно использовать для отдельных устройств. Если приложению toostore другие метаданные для конкретного устройства, его следует использовать хранилище конкретного приложения. Дополнительные сведения см. в [руководстве разработчика по Центру Интернета вещей][lnk-devguide-identity].
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
