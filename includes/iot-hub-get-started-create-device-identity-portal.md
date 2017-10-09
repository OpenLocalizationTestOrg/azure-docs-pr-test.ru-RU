## <a name="create-a-device-identity"></a><span data-ttu-id="75744-101">Создание удостоверения устройства</span><span class="sxs-lookup"><span data-stu-id="75744-101">Create a device identity</span></span>

<span data-ttu-id="75744-102">В этом разделе используется hello [портал Azure] [ lnk-azure-portal] toocreate удостоверение устройства в реестре hello identity в вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="75744-102">In this section, you use hello [Azure portal][lnk-azure-portal] toocreate a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="75744-103">Устройство не удается подключиться tooIoT концентратора, если оно не имеет запись в реестре удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="75744-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="75744-104">Дополнительные сведения см. в разделе hello раздел «Удостоверение реестра» hello [руководстве для разработчиков центра IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="75744-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="75744-105">Hello **обозреватель устройств** hello портал помогает создать уникальный идентификатор устройства и ключ, что устройство может использовать tooidentify себя при соединении tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="75744-105">hello **Device Explorer** in hello portal helps you generate a unique device ID and key that your device can use tooidentify itself when it connects tooIoT Hub.</span></span> <span data-ttu-id="75744-106">Идентификаторы устройств чувствительны к регистру.</span><span class="sxs-lookup"><span data-stu-id="75744-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="75744-107">Убедитесь, что вы вошли в toohello [портал Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="75744-107">Make sure you are signed in toohello [Azure portal][lnk-azure-portal].</span></span>

1. <span data-ttu-id="75744-108">В hello Jumpbar щелкните **все ресурсы** и ресурс концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="75744-108">In hello Jumpbar, click **All resources** and find your IoT hub resource.</span></span>

    ![Перейдите в центр Iot tooyour][img-find-iothub]

1. <span data-ttu-id="75744-110">При открытии ресурса концентратора IoT щелкните hello **обозреватель устройств** инструмент, а затем нажмите кнопку **добавить** вверху hello.</span><span class="sxs-lookup"><span data-stu-id="75744-110">When your IoT hub resource is opened, click hello **Device Explorer** tool, and then click **Add** at hello top.</span></span> <span data-ttu-id="75744-111">Укажите имя hello для нового устройства, например **myDeviceId**и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="75744-111">Provide hello name for your new device, such as **myDeviceId**, and click **Save**.</span></span>

    ![Создание удостоверения устройства на портале][img-create-device]

   <span data-ttu-id="75744-113">После этого будет создано удостоверение устройства для вашего Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="75744-113">This creates a new device identity for your IoT hub.</span></span>

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. <span data-ttu-id="75744-114">В hello **обозреватель устройств**в список устройств, выберите только что созданный hello устройство и запишите hello **строка подключения---первичный ключ**.</span><span class="sxs-lookup"><span data-stu-id="75744-114">In hello **Device Explorer**'s device list, click hello newly created device and make note of hello **Connection string---primary key**.</span></span> 

    ![Строка подключения к устройству.][img-connection-string]

> [!NOTE]
> <span data-ttu-id="75744-116">Hello реестра удостоверений центра IoT хранится только toohello устройства удостоверения tooenable безопасного доступа центра IoT.</span><span class="sxs-lookup"><span data-stu-id="75744-116">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="75744-117">Он сохраняет идентификаторы и ключи toouse устройства как учетные данные безопасности, а также включение или отключение флага, что toodisable доступа можно использовать для отдельных устройств.</span><span class="sxs-lookup"><span data-stu-id="75744-117">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="75744-118">Если приложению toostore другие метаданные для конкретного устройства, его следует использовать хранилище конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="75744-118">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="75744-119">Дополнительные сведения см. в [руководстве разработчика по Центру Интернета вещей][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="75744-119">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

