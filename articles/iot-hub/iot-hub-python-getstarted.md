---
title: "aaaGet работы с Azure IoT Hub (Python) | Документы Microsoft"
description: "Узнайте, как toosend устройства в облако сообщений tooAzure центр IoT с помощью IoT пакеты SDK для Python. Создать имитированное устройство и службы приложений tooregister устройства, отправлять сообщения и чтения сообщений из центра IoT."
services: iot-hub
author: dsk-2015
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: python
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: dkshir
ms.custom: na
ms.openlocfilehash: aa23e792fb144202e121274723bcfaeae0c04723
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a><span data-ttu-id="d326d-104">Подключиться с помощью Python концентратор IoT tooyour имитированное устройство</span><span class="sxs-lookup"><span data-stu-id="d326d-104">Connect your simulated device tooyour IoT hub using Python</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="d326d-105">В конце этого учебника hello будет иметь два приложения Python:</span><span class="sxs-lookup"><span data-stu-id="d326d-105">At hello end of this tutorial, you will have two Python apps:</span></span>

* <span data-ttu-id="d326d-106">**CreateDeviceIdentity.py**, которая создает удостоверения устройства и связана защита ключа tooconnect приложение имитации устройства.</span><span class="sxs-lookup"><span data-stu-id="d326d-106">**CreateDeviceIdentity.py**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="d326d-107">**SimulatedDevice.py**, который подключает tooyour центр IoT с идентификатором hello устройства, созданный ранее и периодически отправляет данные телеметрии сообщений с помощью протокола MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-107">**SimulatedDevice.py**, which connects tooyour IoT hub with hello device identity created earlier, and periodically sends a telemetry message using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="d326d-108">статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild toorun обоих приложений на устройствах и серверной части вашего решения.</span><span class="sxs-lookup"><span data-stu-id="d326d-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="d326d-109">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d326d-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d326d-110">[Python 2.x или 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="d326d-110">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="d326d-111">Сделать убедиться, что toouse hello 32-разрядная или 64-разрядной установки, необходимые настройки.</span><span class="sxs-lookup"><span data-stu-id="d326d-111">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="d326d-112">При появлении запроса во время установки hello сделать убедиться, что переменная среды платформой tooyour tooadd Python.</span><span class="sxs-lookup"><span data-stu-id="d326d-112">When prompted during hello installation, make sure tooadd Python tooyour platform-specific environment variable.</span></span> <span data-ttu-id="d326d-113">При использовании Python 2.x, может потребоваться слишком[Установка или обновление *pip*, hello Python пакета системы управления][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="d326d-113">If you are using Python 2.x, you may need too[install or upgrade *pip*, hello Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="d326d-114">При использовании ОС Windows, затем [распространяемого пакета Visual C++] [ lnk-visual-c-redist] tooallow hello использования собственных библиотек DLL из Python.</span><span class="sxs-lookup"><span data-stu-id="d326d-114">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] tooallow hello use of native DLLs from Python.</span></span>
* <span data-ttu-id="d326d-115">[Node.js 4.0 или более поздней версии][lnk-node-download].</span><span class="sxs-lookup"><span data-stu-id="d326d-115">[Node.js 4.0 or later][lnk-node-download].</span></span> <span data-ttu-id="d326d-116">Сделать убедиться, что toouse hello 32-разрядная или 64-разрядной установки, необходимые настройки.</span><span class="sxs-lookup"><span data-stu-id="d326d-116">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="d326d-117">Это hello необходимые tooinstall [IoT Hub анализатор][lnk-iot-hub-explorer].</span><span class="sxs-lookup"><span data-stu-id="d326d-117">This is needed tooinstall hello [IoT Hub Explorer tool][lnk-iot-hub-explorer].</span></span>
* <span data-ttu-id="d326d-118">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d326d-118">An active Azure account.</span></span> <span data-ttu-id="d326d-119">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d326d-119">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="d326d-120">Hello *pip* пакетов для `azure-iothub-service-client` и `azure-iothub-device-client` в настоящее время доступны только для ОС Windows.</span><span class="sxs-lookup"><span data-stu-id="d326d-120">hello *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="d326d-121">Linux и Mac OS, см. разделы Linux и Mac OS определенного toohello на hello [подготовить среду разработки для Python] [ lnk-python-devbox] post.</span><span class="sxs-lookup"><span data-stu-id="d326d-121">For Linux/Mac OS, please refer toohello Linux and Mac OS-specific sections on hello [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="d326d-122">Теперь Центр Интернета вещей создан.</span><span class="sxs-lookup"><span data-stu-id="d326d-122">You have now created your IoT hub.</span></span> <span data-ttu-id="d326d-123">Используйте hello имя узла Центр IoT и hello центра IoT строку подключения в hello конца данного учебника.</span><span class="sxs-lookup"><span data-stu-id="d326d-123">Use hello IoT Hub host name and hello IoT Hub connection string in hello rest of this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="d326d-124">Концентратор IoT можно также легко создать в командной строке, используя hello Python или Node.js на основе Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d326d-124">You can also easily create your IoT hub on a command line, using hello Python or Node.js based Azure CLI.</span></span> <span data-ttu-id="d326d-125">статья Hello [создать центр IoT с помощью Azure CLI 2.0 hello] [ lnk-azure-cli-hub] hello toodo быстрых действий, поэтому показан.</span><span class="sxs-lookup"><span data-stu-id="d326d-125">hello article [Create an IoT hub using hello Azure CLI 2.0][lnk-azure-cli-hub] shows you hello quick steps toodo so.</span></span> 
> 

## <a name="create-a-device-identity"></a><span data-ttu-id="d326d-126">Создание удостоверения устройства</span><span class="sxs-lookup"><span data-stu-id="d326d-126">Create a device identity</span></span>
<span data-ttu-id="d326d-127">В этом разделе перечислены шаги hello toocreate Python консольного приложения, который создает удостоверение устройства в реестре удостоверений hello концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="d326d-127">This section lists hello steps toocreate a Python console app, that creates a device identity in hello identity registry of your IoT hub.</span></span> <span data-ttu-id="d326d-128">Устройства могут подключаться tooIoT концентратора только в том случае, если он имеет запись в реестре удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-128">A device can only connect tooIoT Hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="d326d-129">Дополнительные сведения см. в разделе hello **реестра удостоверений** раздел hello [руководстве для разработчиков центра IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="d326d-129">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="d326d-130">При запуске это консольное приложение, он создает уникальный идентификатор устройства и ключ, что при отправке устройства в облако, устройство может использовать tooidentify самого сообщения tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="d326d-130">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="d326d-131">Откройте командную строку и установить hello **Azure IoT Hub службы SDK для Python**.</span><span class="sxs-lookup"><span data-stu-id="d326d-131">Open a command prompt and install hello **Azure IoT Hub Service SDK for Python**.</span></span> <span data-ttu-id="d326d-132">Закройте командную строку hello, после установки пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-132">Close hello command prompt after you install hello SDK.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

2. <span data-ttu-id="d326d-133">Создайте файл Python с именем **CreateDeviceIdentity.py**.</span><span class="sxs-lookup"><span data-stu-id="d326d-133">Create a Python file named **CreateDeviceIdentity.py**.</span></span> <span data-ttu-id="d326d-134">Откройте его в [редактора/IDE Python по своему усмотрению][lnk-python-ide-list], Здравствуйте, например, по умолчанию [IDLE][lnk-idle].</span><span class="sxs-lookup"><span data-stu-id="d326d-134">Open it in [a Python editor/IDE of your choice][lnk-python-ide-list], for example, hello default [IDLE][lnk-idle].</span></span>

3. <span data-ttu-id="d326d-135">Добавьте следующий код tooimport hello необходимые модули из пакета SDK службы hello hello:</span><span class="sxs-lookup"><span data-stu-id="d326d-135">Add hello following code tooimport hello required modules from hello service SDK:</span></span>

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. <span data-ttu-id="d326d-136">Добавить hello после кода, заменив заполнитель hello для `[IoTHub Connection String]` со строкой hello подключения для центра IoT hello, созданный в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-136">Add hello following code, replacing hello placeholder for `[IoTHub Connection String]` with hello connection string for hello IoT hub you created in hello previous section.</span></span> <span data-ttu-id="d326d-137">Можно использовать любое имя, как hello `DEVICE_ID`.</span><span class="sxs-lookup"><span data-stu-id="d326d-137">You can use any name as hello `DEVICE_ID`.</span></span>
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. <span data-ttu-id="d326d-138">Добавить hello следующие функции tooprint часть сведений об устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-138">Add hello following function tooprint some of hello device information.</span></span>

    ```python
    def print_device_info(title, iothub_device):
        print ( title + ":" )
        print ( "iothubDevice.deviceId                    = {0}".format(iothub_device.deviceId) )
        print ( "iothubDevice.primaryKey                  = {0}".format(iothub_device.primaryKey) )
        print ( "iothubDevice.secondaryKey                = {0}".format(iothub_device.secondaryKey) )
        print ( "iothubDevice.connectionState             = {0}".format(iothub_device.connectionState) )
        print ( "iothubDevice.status                      = {0}".format(iothub_device.status) )
        print ( "iothubDevice.lastActivityTime            = {0}".format(iothub_device.lastActivityTime) )
        print ( "iothubDevice.cloudToDeviceMessageCount   = {0}".format(iothub_device.cloudToDeviceMessageCount) )
        print ( "iothubDevice.isManaged                   = {0}".format(iothub_device.isManaged) )
        print ( "iothubDevice.authMethod                  = {0}".format(iothub_device.authMethod) )
        print ( "" )
    ```
3. <span data-ttu-id="d326d-139">Добавьте следующие функции toocreate hello устройства идентификации с помощью hello диспетчер реестра hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-139">Add hello following function toocreate hello device identification using hello Registry Manager.</span></span> 

    ```python
    def iothub_createdevice():
        try:
            iothub_registry_manager = IoTHubRegistryManager(CONNECTION_STRING)
            auth_method = IoTHubRegistryManagerAuthMethod.SHARED_PRIVATE_KEY
            new_device = iothub_registry_manager.create_device(DEVICE_ID, "", "", auth_method)
            print_device_info("CreateDevice", new_device)

        except IoTHubError as iothub_error:
            print ( "Unexpected error {0}".format(iothub_error) )
            return
        except KeyboardInterrupt:
            print ( "iothub_createdevice stopped" )
    ```
4. <span data-ttu-id="d326d-140">Наконец добавьте функцию main hello, как показано ниже и сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-140">Finally, add hello main function as follows and save hello file.</span></span>

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using hello Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. <span data-ttu-id="d326d-141">На hello командной строки, запустите hello **CreateDeviceIdentity.py** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d326d-141">On hello command prompt, run hello **CreateDeviceIdentity.py** as follows:</span></span>

    ```python
    python CreateDeviceIdentity.py
    ```
6. <span data-ttu-id="d326d-142">Вы увидите начало создать имитированное устройство hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-142">You should see hello simulated device getting created.</span></span> <span data-ttu-id="d326d-143">Запишите hello **deviceId** и hello **primaryKey** этого устройства.</span><span class="sxs-lookup"><span data-stu-id="d326d-143">Note down hello **deviceId** and hello **primaryKey** of this device.</span></span> <span data-ttu-id="d326d-144">Эти значения должны позже при создании приложения, которое подключается tooIoT концентратора как устройство.</span><span class="sxs-lookup"><span data-stu-id="d326d-144">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

    ![Успешное создание устройства][1]

> [!NOTE]
> <span data-ttu-id="d326d-146">Hello реестра удостоверений центра IoT хранится только toohello устройства удостоверения tooenable безопасного доступа центра IoT.</span><span class="sxs-lookup"><span data-stu-id="d326d-146">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="d326d-147">Он сохраняет идентификаторы и ключи toouse устройства как учетные данные безопасности и включение или отключение флага, что toodisable доступа можно использовать для отдельных устройств.</span><span class="sxs-lookup"><span data-stu-id="d326d-147">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="d326d-148">Если приложению toostore другие метаданные для конкретного устройства, его следует использовать хранилище конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="d326d-148">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="d326d-149">Дополнительные сведения см. в разделе hello [руководстве для разработчиков центра IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="d326d-149">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="d326d-150">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="d326d-150">Create a simulated device app</span></span>
<span data-ttu-id="d326d-151">В этом разделе перечислены шаги hello toocreate консольное приложение Python, которое имитирует устройство и отправляет сообщения из устройства в облако центра IoT tooyour.</span><span class="sxs-lookup"><span data-stu-id="d326d-151">This section lists hello steps toocreate a Python console app, that simulates a device and sends device-to-cloud messages tooyour IoT hub.</span></span>

1. <span data-ttu-id="d326d-152">Откройте новую командную строку и установите hello Azure IoT Hub устройства SDK для Python следующим образом.</span><span class="sxs-lookup"><span data-stu-id="d326d-152">Open a new command prompt and install hello Azure IoT Hub Device SDK for Python as follows.</span></span> <span data-ttu-id="d326d-153">Закройте командную строку hello после установки hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-153">Close hello command prompt after hello installation.</span></span>

    ```
    pip install azure-iothub-device-client
    ```
2. <span data-ttu-id="d326d-154">Создайте файл с именем **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="d326d-154">Create a file named **SimulatedDevice.py**.</span></span> <span data-ttu-id="d326d-155">Откройте его в редакторе или интегрированной среде разработки Python (например, IDLE).</span><span class="sxs-lookup"><span data-stu-id="d326d-155">Open this file in a Python editor/IDE of your choice (for example, IDLE).</span></span>

3. <span data-ttu-id="d326d-156">Добавьте следующую hello необходимые модули кода tooimport из SDK устройства hello hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-156">Add hello following code tooimport hello required modules from hello device SDK.</span></span>

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. <span data-ttu-id="d326d-157">Добавить hello следующим кодом и замените заполнитель hello для `[IoTHub Device Connection String]` со строкой hello подключения для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="d326d-157">Add hello following code and replace hello placeholder for `[IoTHub Device Connection String]` with hello connection string for your device.</span></span> <span data-ttu-id="d326d-158">Строка подключения устройства Hello, обычно имеет формат hello объекта `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span><span class="sxs-lookup"><span data-stu-id="d326d-158">hello device connection string is usually in hello format of `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span></span> <span data-ttu-id="d326d-159">Используйте hello **deviceId** и **primaryKey** hello устройства, созданный в hello предыдущего раздела tooreplace hello `<deviceId>` и `<primaryKey>` соответственно.</span><span class="sxs-lookup"><span data-stu-id="d326d-159">Use hello **deviceId** and **primaryKey** of hello device you created in hello previous section tooreplace hello `<deviceId>` and `<primaryKey>` respectively.</span></span> <span data-ttu-id="d326d-160">Замените `<hostName>` именем узла Центра Интернета вещей (обычно это `<IoT hub name>.azure-devices.net`).</span><span class="sxs-lookup"><span data-stu-id="d326d-160">Replace `<hostName>` with your IoT hub's host name, usually as `<IoT hub name>.azure-devices.net`.</span></span>

    ```python
    # String containing Hostname, Device Id & Device Key in hello format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. <span data-ttu-id="d326d-161">Добавьте следующий код toodefine обратный вызов подтверждения отправки hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-161">Add hello following code toodefine a send confirmation callback.</span></span> 

    ```python
    def send_confirmation_callback(message, result, user_context):
        global SEND_CALLBACKS
        print ( "Confirmation[%d] received for message with result = %s" % (user_context, result) )
        map_properties = message.properties()
        print ( "    message_id: %s" % message.message_id )
        print ( "    correlation_id: %s" % message.correlation_id )
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        SEND_CALLBACKS += 1
        print ( "    Total calls confirmed: %d" % SEND_CALLBACKS )
    ```
6. <span data-ttu-id="d326d-162">Добавьте следующий код tooinitialize hello устройства клиента hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-162">Add hello following code tooinitialize hello device client.</span></span>

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. <span data-ttu-id="d326d-163">Добавьте следующие hello функцией tooformat и отправки сообщения из вашего центра IoT tooyour имитированное устройство.</span><span class="sxs-lookup"><span data-stu-id="d326d-163">Add hello following function tooformat and send a message from your simulated device tooyour IoT hub.</span></span>

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C tooexit" )
            message_counter = 0

            while True:
                msg_txt_formatted = MSG_TXT % (AVG_WIND_SPEED + (random.random() * 4 + 2))
                # messages can be encoded as string or bytearray
                if (message_counter & 1) == 1:
                    message = IoTHubMessage(bytearray(msg_txt_formatted, 'utf8'))
                else:
                    message = IoTHubMessage(msg_txt_formatted)
                # optional: assign ids
                message.message_id = "message_%d" % message_counter
                message.correlation_id = "correlation_%d" % message_counter
                # optional: assign properties
                prop_map = message.properties()
                prop_text = "PropMsg_%d" % message_counter
                prop_map.add("Property", prop_text)

                client.send_event_async(message, send_confirmation_callback, message_counter)
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission tooIoT Hub." % message_counter )

                status = client.get_send_status()
                print ( "Send status: %s" % status )
                time.sleep(30)

                status = client.get_send_status()
                print ( "Send status: %s" % status )

                message_counter += 1

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )
    ```
8. <span data-ttu-id="d326d-164">Наконец добавьте основной функции hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-164">Finally, add hello main function.</span></span> 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. <span data-ttu-id="d326d-165">Сохраните и закройте hello **SimulatedDevice.py** файла.</span><span class="sxs-lookup"><span data-stu-id="d326d-165">Save and close hello **SimulatedDevice.py** file.</span></span> <span data-ttu-id="d326d-166">Вы являются теперь готовы toorun это приложение.</span><span class="sxs-lookup"><span data-stu-id="d326d-166">You are now ready toorun this app.</span></span>

> [!NOTE]
> <span data-ttu-id="d326d-167">простые действия tookeep, этот учебник не реализует никакую политику повтора.</span><span class="sxs-lookup"><span data-stu-id="d326d-167">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d326d-168">В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="d326d-168">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a><span data-ttu-id="d326d-169">Получение сообщений с виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="d326d-169">Receive messages from your simulated device</span></span>
<span data-ttu-id="d326d-170">tooreceive телеметрии сообщения с устройства, необходимо toouse [концентраторов событий][lnk-event-hubs-overview]-совместимый конечная точка, предоставляемая hello центра IoT, который считывает сообщения из устройства в облако hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-170">tooreceive telemetry messages from your device, you need toouse an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint exposed by hello IoT Hub, which reads hello device-to-cloud messages.</span></span> <span data-ttu-id="d326d-171">Чтение hello [Приступая к работе с концентраторами событий] [ lnk-eventhubs-tutorial] учебника сведения о способ tooprocess сообщений из концентраторов событий для конечной точки центра IoT совместимое концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="d326d-171">Read hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial for information on how tooprocess messages from Event Hubs for your IoT hub's Event Hub-compatible endpoint.</span></span> <span data-ttu-id="d326d-172">Концентраторы событий еще не поддерживает телеметрии в Python, поэтому можно либо создать [Node.js](iot-hub-node-node-getstarted.md#D2C_node) или [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) сообщения консоли на основе концентраторов событий приложения tooread hello устройства в облако из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="d326d-172">Event Hubs does not support telemetry in Python yet, so you can either create a [Node.js](iot-hub-node-node-getstarted.md#D2C_node) or a [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs-based console app tooread hello device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="d326d-173">В этом учебнике показано, как можно использовать hello [IoT Hub анализатор] [ lnk-iot-hub-explorer] tooread эти сообщения устройства.</span><span class="sxs-lookup"><span data-stu-id="d326d-173">This tutorial shows how you can use hello [IoT Hub Explorer tool][lnk-iot-hub-explorer] tooread these device messages.</span></span>

1. <span data-ttu-id="d326d-174">Откройте командную строку и установите hello Explorer концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="d326d-174">Open a command prompt and install hello IoT Hub Explorer.</span></span> 

    ```
    npm install -g iothub-explorer
    ```

2. <span data-ttu-id="d326d-175">Запустите следующую команду в командной строке hello hello, наблюдение за toobegin hello сообщения из устройства в облако с устройства.</span><span class="sxs-lookup"><span data-stu-id="d326d-175">Run hello following command on hello command prompt, toobegin monitoring hello device-to-cloud messages from your device.</span></span> <span data-ttu-id="d326d-176">Использовать центр IoT строку подключения в заполнитель hello после `--login`.</span><span class="sxs-lookup"><span data-stu-id="d326d-176">Use your IoT hub's connection string in hello placeholder after `--login`.</span></span>

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. <span data-ttu-id="d326d-177">Откройте новую командную строку и перейдите в каталог toohello, содержащий hello **SimulatedDevice.py** файла.</span><span class="sxs-lookup"><span data-stu-id="d326d-177">Open a new command prompt and navigate toohello directory containing hello **SimulatedDevice.py** file.</span></span>

4. <span data-ttu-id="d326d-178">Запустите hello **SimulatedDevice.py** файл, который периодически отправляет центр IoT tooyour данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="d326d-178">Run hello **SimulatedDevice.py** file, which periodically sends telemetry data tooyour IoT hub.</span></span> 
   
    ```
    python SimulatedDevice.py
    ```
5. <span data-ttu-id="d326d-179">Просмотрите сообщения hello устройства на hello командной строки hello Explorer концентратора IoT hello в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="d326d-179">Observe hello device messages on hello command prompt running hello IoT Hub Explorer from hello previous section.</span></span> 

    ![Сообщения Python, отправляемые с устройства в облако][2]

## <a name="next-steps"></a><span data-ttu-id="d326d-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d326d-181">Next steps</span></span>
<span data-ttu-id="d326d-182">В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="d326d-183">Вы использовали устройства удостоверения tooenable hello имитируемые устройства приложения toosend сообщения из устройства в облако toohello центр IoT.</span><span class="sxs-lookup"><span data-stu-id="d326d-183">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="d326d-184">Вы заметили hello сообщений, полученных hello центр IoT с помощью средства обозревателя концентратора IoT hello hello.</span><span class="sxs-lookup"><span data-stu-id="d326d-184">You observed hello messages received by hello IoT hub with hello help of hello IoT Hub Explorer tool.</span></span> 

<span data-ttu-id="d326d-185">Посетите tooexplore hello Python SDK для использования Azure IoT Hub подробно, [репозиторий Git концентратора][lnk-python-github].</span><span class="sxs-lookup"><span data-stu-id="d326d-185">tooexplore hello Python SDK for Azure IoT Hub usage in depth, visit [this Git Hub repo][lnk-python-github].</span></span> <span data-ttu-id="d326d-186">tooreview hello возможности обмена сообщениями hello Azure IoT Hub службы SDK для Python, можно загрузить и запустить [iothub_messaging_sample.py][lnk-messaging-sample].</span><span class="sxs-lookup"><span data-stu-id="d326d-186">tooreview hello messaging capabilities of hello Azure IoT Hub Service SDK for Python, you can download and run [iothub_messaging_sample.py][lnk-messaging-sample].</span></span> <span data-ttu-id="d326d-187">Для имитации сторона устройства с помощью hello Azure IoT Hub устройства SDK для Python, можно загрузить и запустить hello [iothub_client_sample.py][lnk-client-sample].</span><span class="sxs-lookup"><span data-stu-id="d326d-187">For device side simulation using hello Azure IoT Hub Device SDK for Python, you can download and run hello [iothub_client_sample.py][lnk-client-sample].</span></span>

<span data-ttu-id="d326d-188">Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:</span><span class="sxs-lookup"><span data-stu-id="d326d-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="d326d-189">[Подключение устройства к Azure IoT][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="d326d-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="d326d-190">[How to get started with device management (Node)][lnk-device-management] (Начало работы с управлением устройствами (Node))</span><span class="sxs-lookup"><span data-stu-id="d326d-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="d326d-191">[Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Приступая к работе с архитектурой Azure IoT Edge в Linux)</span><span class="sxs-lookup"><span data-stu-id="d326d-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="d326d-192">toolearn tooextend сообщений в масштабе, IoT решение и процесс устройства в облако. в статье hello [обрабатывать сообщения из устройства в облако] [ lnk-process-d2c-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="d326d-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[1]: ./media/iot-hub-python-getstarted/createdevice.png
[2]: ./media/iot-hub-python-getstarted/sendd2cmessage.png

<!-- Links -->
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-node-download]: https://nodejs.org/en/download/
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
[lnk-azure-cli-hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-using-cli
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-idle]: https://docs.python.org/3/library/idle.html
[lnk-python-ide-list]: https://wiki.python.org/moin/IntegratedDevelopmentEnvironments
[lnk-iot-hub-explorer]: https://github.com/Azure/iothub-explorer
[lnk-python-github]: https://github.com/Azure/azure-iot-sdk-python
[lnk-messaging-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/service/samples/iothub_messaging_sample.py
[lnk-client-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/device/samples/iothub_client_sample.py

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-python-devbox]: https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md

[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
