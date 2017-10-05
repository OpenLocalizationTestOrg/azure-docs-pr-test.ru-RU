---
title: "Приступая к работе с Центром Интернета вещей Azure (Python) | Документация Майкрософт"
description: "Узнайте, как отправлять сообщения из устройства на облако в Центр Интернета вещей Azure с помощью пакетов SDK Интернета вещей для Python. Создайте виртуальное устройство и приложения службы для регистрации устройства, отправки сообщений и чтения сообщений из Центра Интернета вещей."
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
ms.openlocfilehash: 7ebbac4464d793717f68a4cb7905c53d1f5c051a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-simulated-device-to-your-iot-hub-using-python"></a><span data-ttu-id="dac28-104">Подключение виртуального устройства к Центру Интернета вещей с помощью Python</span><span class="sxs-lookup"><span data-stu-id="dac28-104">Connect your simulated device to your IoT hub using Python</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="dac28-105">По завершении работы с этим руководством у вас будет два приложения Python:</span><span class="sxs-lookup"><span data-stu-id="dac28-105">At the end of this tutorial, you will have two Python apps:</span></span>

* <span data-ttu-id="dac28-106">**CreateDeviceIdentity.py** — создает удостоверение устройства и соответствующий ключ безопасности для подключения к приложению виртуального устройства.</span><span class="sxs-lookup"><span data-stu-id="dac28-106">**CreateDeviceIdentity.py**, which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="dac28-107">**SimulatedDevice.py** — подключается к Центру Интернета вещей с созданным ранее удостоверением устройства и периодически отправляет сообщения телеметрии с использованием протокола MQTT.</span><span class="sxs-lookup"><span data-stu-id="dac28-107">**SimulatedDevice.py**, which connects to your IoT hub with the device identity created earlier, and periodically sends a telemetry message using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="dac28-108">Статья о [пакетах SDK для Центра Интернета вещей Azure][lnk-hub-sdks] содержит сведения о различных пакетах SDK, которые можно использовать для создания приложений, которые будут работать на устройствах и в серверной части решения.</span><span class="sxs-lookup"><span data-stu-id="dac28-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="dac28-109">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="dac28-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="dac28-110">[Python 2.x или 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="dac28-110">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="dac28-111">Обязательно используйте 32-разрядную или 64-разрядную версию установки согласно требованиям программы настройки.</span><span class="sxs-lookup"><span data-stu-id="dac28-111">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="dac28-112">При появлении запроса во время установки обязательно добавьте Python в переменную среды соответствующей платформы.</span><span class="sxs-lookup"><span data-stu-id="dac28-112">When prompted during the installation, make sure to add Python to your platform-specific environment variable.</span></span> <span data-ttu-id="dac28-113">Если вы используете Python 2.x, может потребоваться [установка или обновление *pip* — системы управления пакетами Python][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="dac28-113">If you are using Python 2.x, you may need to [install or upgrade *pip*, the Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="dac28-114">При использовании ОС Windows потребуется [распространяемый пакет Visual C++][lnk-visual-c-redist], чтобы разрешить использовать встроенные библиотеки DLL из Python.</span><span class="sxs-lookup"><span data-stu-id="dac28-114">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] to allow the use of native DLLs from Python.</span></span>
* <span data-ttu-id="dac28-115">[Node.js 4.0 или более поздней версии][lnk-node-download].</span><span class="sxs-lookup"><span data-stu-id="dac28-115">[Node.js 4.0 or later][lnk-node-download].</span></span> <span data-ttu-id="dac28-116">Обязательно используйте 32-разрядную или 64-разрядную версию установки согласно требованиям программы настройки.</span><span class="sxs-lookup"><span data-stu-id="dac28-116">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="dac28-117">Это необходимо для установки [средства обозревателя Центра Интернета вещей][lnk-iot-hub-explorer].</span><span class="sxs-lookup"><span data-stu-id="dac28-117">This is needed to install the [IoT Hub Explorer tool][lnk-iot-hub-explorer].</span></span>
* <span data-ttu-id="dac28-118">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="dac28-118">An active Azure account.</span></span> <span data-ttu-id="dac28-119">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="dac28-119">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="dac28-120">Сейчас пакеты *pip* для `azure-iothub-service-client` и `azure-iothub-device-client` доступны только для ОС Windows.</span><span class="sxs-lookup"><span data-stu-id="dac28-120">The *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="dac28-121">Сведения для ОС Linux и Mac см. в соответствующих разделах статьи [Prepare your development environment][lnk-python-devbox] (Подготовка среды разработки).</span><span class="sxs-lookup"><span data-stu-id="dac28-121">For Linux/Mac OS, please refer to the Linux and Mac OS-specific sections on the [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="dac28-122">Теперь центр IoT создан</span><span class="sxs-lookup"><span data-stu-id="dac28-122">You have now created your IoT hub.</span></span> <span data-ttu-id="dac28-123">Используйте имя узла и строку подключения Центра Интернета вещей в оставшейся части этого руководства.</span><span class="sxs-lookup"><span data-stu-id="dac28-123">Use the IoT Hub host name and the IoT Hub connection string in the rest of this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="dac28-124">Центр Интернета вещей также можно легко создать в командной строке с помощью Python или Node.js на основе Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="dac28-124">You can also easily create your IoT hub on a command line, using the Python or Node.js based Azure CLI.</span></span> <span data-ttu-id="dac28-125">Дополнительные сведения о том, как это сделать быстро, см. в статье [Создание Центра Интернета вещей с помощью Azure CLI 2.0][lnk-azure-cli-hub].</span><span class="sxs-lookup"><span data-stu-id="dac28-125">The article [Create an IoT hub using the Azure CLI 2.0][lnk-azure-cli-hub] shows you the quick steps to do so.</span></span> 
> 

## <a name="create-a-device-identity"></a><span data-ttu-id="dac28-126">Создание удостоверения устройства</span><span class="sxs-lookup"><span data-stu-id="dac28-126">Create a device identity</span></span>
<span data-ttu-id="dac28-127">В этом разделе приведены инструкции по написанию консольного приложения Python, создающего удостоверение устройства в реестре удостоверений Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="dac28-127">This section lists the steps to create a Python console app, that creates a device identity in the identity registry of your IoT hub.</span></span> <span data-ttu-id="dac28-128">Устройство может подключиться к Центру Интернета вещей, только если в реестре удостоверений есть соответствующая запись.</span><span class="sxs-lookup"><span data-stu-id="dac28-128">A device can only connect to IoT Hub if it has an entry in the identity registry.</span></span> <span data-ttu-id="dac28-129">Дополнительные сведения см. в разделе, посвященном **реестру удостоверений**, в [руководстве разработчика по Центру Интернета вещей Azure][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="dac28-129">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="dac28-130">При запуске этого консольного приложения создается уникальный идентификатор устройства и ключ, с помощью которых выполняется идентификация во время отправки сообщений из устройства в облако для центра IoT.</span><span class="sxs-lookup"><span data-stu-id="dac28-130">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="dac28-131">Откройте окно командной строки и установите **пакет SDK службы Центра Интернета вещей Azure для Python**.</span><span class="sxs-lookup"><span data-stu-id="dac28-131">Open a command prompt and install the **Azure IoT Hub Service SDK for Python**.</span></span> <span data-ttu-id="dac28-132">После установки пакета SDK закройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="dac28-132">Close the command prompt after you install the SDK.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

2. <span data-ttu-id="dac28-133">Создайте файл Python с именем **CreateDeviceIdentity.py**.</span><span class="sxs-lookup"><span data-stu-id="dac28-133">Create a Python file named **CreateDeviceIdentity.py**.</span></span> <span data-ttu-id="dac28-134">Откройте его в [редакторе или интегрированной среде разработки Python][lnk-python-ide-list] (например, [IDLE][lnk-idle] по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="dac28-134">Open it in [a Python editor/IDE of your choice][lnk-python-ide-list], for example, the default [IDLE][lnk-idle].</span></span>

3. <span data-ttu-id="dac28-135">Добавьте следующий код для импорта необходимых модулей из пакета SDK службы:</span><span class="sxs-lookup"><span data-stu-id="dac28-135">Add the following code to import the required modules from the service SDK:</span></span>

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. <span data-ttu-id="dac28-136">Добавьте следующий код, заменив заполнитель `[IoTHub Connection String]` строкой подключения для Центра Интернета вещей, созданного в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="dac28-136">Add the following code, replacing the placeholder for `[IoTHub Connection String]` with the connection string for the IoT hub you created in the previous section.</span></span> <span data-ttu-id="dac28-137">Вы можете использовать любое имя, например `DEVICE_ID`.</span><span class="sxs-lookup"><span data-stu-id="dac28-137">You can use any name as the `DEVICE_ID`.</span></span>
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. <span data-ttu-id="dac28-138">Добавьте следующую функцию для вывода некоторых сведений об устройстве.</span><span class="sxs-lookup"><span data-stu-id="dac28-138">Add the following function to print some of the device information.</span></span>

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
3. <span data-ttu-id="dac28-139">Добавьте следующую функцию, чтобы установить идентификацию устройства с помощью диспетчера реестра.</span><span class="sxs-lookup"><span data-stu-id="dac28-139">Add the following function to create the device identification using the Registry Manager.</span></span> 

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
4. <span data-ttu-id="dac28-140">Теперь добавьте функцию main, как показано ниже, и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="dac28-140">Finally, add the main function as follows and save the file.</span></span>

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using the Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. <span data-ttu-id="dac28-141">В командной строке запустите **CreateDeviceIdentity.py** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dac28-141">On the command prompt, run the **CreateDeviceIdentity.py** as follows:</span></span>

    ```python
    python CreateDeviceIdentity.py
    ```
6. <span data-ttu-id="dac28-142">Виртуальное устройство должно начать создаваться.</span><span class="sxs-lookup"><span data-stu-id="dac28-142">You should see the simulated device getting created.</span></span> <span data-ttu-id="dac28-143">Запишите значения устройства **deviceId** и **primaryKey**.</span><span class="sxs-lookup"><span data-stu-id="dac28-143">Note down the **deviceId** and the **primaryKey** of this device.</span></span> <span data-ttu-id="dac28-144">Эти значения понадобятся вам позже, когда вы будете создавать приложение, которое подключается к центру IoT как устройство.</span><span class="sxs-lookup"><span data-stu-id="dac28-144">You need these values later when you create an application that connects to IoT Hub as a device.</span></span>

    ![Успешное создание устройства][1]

> [!NOTE]
> <span data-ttu-id="dac28-146">В реестре удостоверений в Центре Интернета вещей хранятся только идентификаторы устройств, необходимые для безопасного доступа к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="dac28-146">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="dac28-147">В этом реестре хранятся идентификаторы и ключи устройств, которые используются в качестве учетных данных безопасности, и флажок включения или выключения, который позволяет вам отключить доступ для отдельного устройства.</span><span class="sxs-lookup"><span data-stu-id="dac28-147">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="dac28-148">Если в приложении необходимо хранить другие метаданные для конкретного устройства, следует использовать хранилище конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="dac28-148">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="dac28-149">Дополнительные сведения см. в [руководстве для разработчиков Центра Интернета вещей][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="dac28-149">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="dac28-150">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="dac28-150">Create a simulated device app</span></span>
<span data-ttu-id="dac28-151">В этом разделе приведены инструкции по созданию консольного приложения Python, имитирующего устройство и отправляющего сообщения с устройства в облако в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="dac28-151">This section lists the steps to create a Python console app, that simulates a device and sends device-to-cloud messages to your IoT hub.</span></span>

1. <span data-ttu-id="dac28-152">Откройте новое окно командной строки и установите пакет SDK устройства Центра Интернета вещей Azure для Python указанным ниже образом.</span><span class="sxs-lookup"><span data-stu-id="dac28-152">Open a new command prompt and install the Azure IoT Hub Device SDK for Python as follows.</span></span> <span data-ttu-id="dac28-153">После установки закройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="dac28-153">Close the command prompt after the installation.</span></span>

    ```
    pip install azure-iothub-device-client
    ```
2. <span data-ttu-id="dac28-154">Создайте файл с именем **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="dac28-154">Create a file named **SimulatedDevice.py**.</span></span> <span data-ttu-id="dac28-155">Откройте его в редакторе или интегрированной среде разработки Python (например, IDLE).</span><span class="sxs-lookup"><span data-stu-id="dac28-155">Open this file in a Python editor/IDE of your choice (for example, IDLE).</span></span>

3. <span data-ttu-id="dac28-156">Добавьте следующий код для импорта необходимых модулей из пакета SDK устройства.</span><span class="sxs-lookup"><span data-stu-id="dac28-156">Add the following code to import the required modules from the device SDK.</span></span>

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. <span data-ttu-id="dac28-157">Добавьте следующий код и замените заполнитель `[IoTHub Device Connection String]` строкой подключения для устройства.</span><span class="sxs-lookup"><span data-stu-id="dac28-157">Add the following code and replace the placeholder for `[IoTHub Device Connection String]` with the connection string for your device.</span></span> <span data-ttu-id="dac28-158">Обычно строка подключения устройства указывается в формате `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span><span class="sxs-lookup"><span data-stu-id="dac28-158">The device connection string is usually in the format of `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span></span> <span data-ttu-id="dac28-159">Используйте значения **deviceId** и **primaryKey** устройства, созданного в предыдущем разделе, чтобы заменить `<deviceId>` и `<primaryKey>` соответственно.</span><span class="sxs-lookup"><span data-stu-id="dac28-159">Use the **deviceId** and **primaryKey** of the device you created in the previous section to replace the `<deviceId>` and `<primaryKey>` respectively.</span></span> <span data-ttu-id="dac28-160">Замените `<hostName>` именем узла Центра Интернета вещей (обычно это `<IoT hub name>.azure-devices.net`).</span><span class="sxs-lookup"><span data-stu-id="dac28-160">Replace `<hostName>` with your IoT hub's host name, usually as `<IoT hub name>.azure-devices.net`.</span></span>

    ```python
    # String containing Hostname, Device Id & Device Key in the format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. <span data-ttu-id="dac28-161">Добавьте следующий код, чтобы определить обратный вызов подтверждения отправки.</span><span class="sxs-lookup"><span data-stu-id="dac28-161">Add the following code to define a send confirmation callback.</span></span> 

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
6. <span data-ttu-id="dac28-162">Добавьте следующий код для инициализации клиента устройства.</span><span class="sxs-lookup"><span data-stu-id="dac28-162">Add the following code to initialize the device client.</span></span>

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set the time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. <span data-ttu-id="dac28-163">Добавьте следующую функцию для форматирования и отправки сообщения из виртуального устройства в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="dac28-163">Add the following function to format and send a message from your simulated device to your IoT hub.</span></span>

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C to exit" )
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
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission to IoT Hub." % message_counter )

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
8. <span data-ttu-id="dac28-164">Теперь добавьте функцию main.</span><span class="sxs-lookup"><span data-stu-id="dac28-164">Finally, add the main function.</span></span> 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using the Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. <span data-ttu-id="dac28-165">Сохраните и закройте файл **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="dac28-165">Save and close the **SimulatedDevice.py** file.</span></span> <span data-ttu-id="dac28-166">Теперь все готово к запуску приложения.</span><span class="sxs-lookup"><span data-stu-id="dac28-166">You are now ready to run this app.</span></span>

> [!NOTE]
> <span data-ttu-id="dac28-167">Для простоты в этом руководстве не реализуются политики повтора.</span><span class="sxs-lookup"><span data-stu-id="dac28-167">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="dac28-168">В рабочем коде следует реализовать политики повторных попыток (например, с экспоненциальной задержкой), как указано в статье [Обработка временного сбоя][lnk-transient-faults] на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="dac28-168">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a><span data-ttu-id="dac28-169">Получение сообщений с виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="dac28-169">Receive messages from your simulated device</span></span>
<span data-ttu-id="dac28-170">Для получения сообщений телеметрии с устройства необходимо использовать совместимую с [концентраторами событий][lnk-event-hubs-overview] конечную точку, предоставляемую Центром Интернета вещей, которая считывает сообщения, отправляемые с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="dac28-170">To receive telemetry messages from your device, you need to use an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint exposed by the IoT Hub, which reads the device-to-cloud messages.</span></span> <span data-ttu-id="dac28-171">Ознакомьтесь с руководством по [началу работы с концентраторами событий][lnk-eventhubs-tutorial], чтобы узнать, как обрабатываются сообщения из концентраторов событий для конечной точки Центра Интернета вещей, совместимой с концентраторами событий.</span><span class="sxs-lookup"><span data-stu-id="dac28-171">Read the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial for information on how to process messages from Event Hubs for your IoT hub's Event Hub-compatible endpoint.</span></span> <span data-ttu-id="dac28-172">Концентраторы событий пока не поддерживают данные телеметрии на языке Python. Таким образом, вы можете создать консольное приложение [Node.js](iot-hub-node-node-getstarted.md#D2C_node) или [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) на основе концентраторов событий для чтения сообщений, отправляемых с устройства в облако, из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="dac28-172">Event Hubs does not support telemetry in Python yet, so you can either create a [Node.js](iot-hub-node-node-getstarted.md#D2C_node) or a [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs-based console app to read the device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="dac28-173">В этом руководстве описывается, как использовать [средство обозревателя Центра Интернета вещей][lnk-iot-hub-explorer] для чтения этих сообщений с устройства.</span><span class="sxs-lookup"><span data-stu-id="dac28-173">This tutorial shows how you can use the [IoT Hub Explorer tool][lnk-iot-hub-explorer] to read these device messages.</span></span>

1. <span data-ttu-id="dac28-174">Откройте окно командной строки и установите обозреватель Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="dac28-174">Open a command prompt and install the IoT Hub Explorer.</span></span> 

    ```
    npm install -g iothub-explorer
    ```

2. <span data-ttu-id="dac28-175">В командной строке выполните следующую команду, чтобы начать мониторинг сообщений, отправляемых с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="dac28-175">Run the following command on the command prompt, to begin monitoring the device-to-cloud messages from your device.</span></span> <span data-ttu-id="dac28-176">Используйте строку подключения Центра Интернета вещей в заполнителе после `--login`.</span><span class="sxs-lookup"><span data-stu-id="dac28-176">Use your IoT hub's connection string in the placeholder after `--login`.</span></span>

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. <span data-ttu-id="dac28-177">Откройте новое окно командной строки и перейдите к каталогу, содержащему файл **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="dac28-177">Open a new command prompt and navigate to the directory containing the **SimulatedDevice.py** file.</span></span>

4. <span data-ttu-id="dac28-178">Запустите файл **SimulatedDevice.py**, который периодически отправляет данные телеметрии в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="dac28-178">Run the **SimulatedDevice.py** file, which periodically sends telemetry data to your IoT hub.</span></span> 
   
    ```
    python SimulatedDevice.py
    ```
5. <span data-ttu-id="dac28-179">Просмотрите сообщения с устройства в командной строке, запущенной обозревателем Центра Интернета вещей, из предыдущего раздела.</span><span class="sxs-lookup"><span data-stu-id="dac28-179">Observe the device messages on the command prompt running the IoT Hub Explorer from the previous section.</span></span> 

    ![Сообщения Python, отправляемые с устройства в облако][2]

## <a name="next-steps"></a><span data-ttu-id="dac28-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dac28-181">Next steps</span></span>
<span data-ttu-id="dac28-182">В этом руководстве мы настроили новый Центр Интернета вещей на портале Azure и создали удостоверение устройства в реестре удостоверений Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="dac28-182">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="dac28-183">Это удостоверение позволяет приложению виртуального устройства отправлять в Центр Интернета вещей сообщения, передаваемые из устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="dac28-183">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="dac28-184">Мы просмотрели сообщения, полученные Центром Интернета вещей, с помощью средства обозревателя.</span><span class="sxs-lookup"><span data-stu-id="dac28-184">You observed the messages received by the IoT hub with the help of the IoT Hub Explorer tool.</span></span> 

<span data-ttu-id="dac28-185">Чтобы узнать больше об использовании пакета SDK Python для Центра Интернета вещей Azure, перейдите на страницу [этого репозитория GitHub][lnk-python-github].</span><span class="sxs-lookup"><span data-stu-id="dac28-185">To explore the Python SDK for Azure IoT Hub usage in depth, visit [this Git Hub repo][lnk-python-github].</span></span> <span data-ttu-id="dac28-186">Чтобы просмотреть возможности обмена сообщениями пакета SDK службы Центра Интернета вещей Azure для Python, можно скачать и запустить [iothub_messaging_sample.py][lnk-messaging-sample].</span><span class="sxs-lookup"><span data-stu-id="dac28-186">To review the messaging capabilities of the Azure IoT Hub Service SDK for Python, you can download and run [iothub_messaging_sample.py][lnk-messaging-sample].</span></span> <span data-ttu-id="dac28-187">Для имитации устройства с помощью пакета SDK устройства Центра Интернета вещей Azure для Python можно скачать и запустить [iothub_client_sample.py][lnk-client-sample].</span><span class="sxs-lookup"><span data-stu-id="dac28-187">For device side simulation using the Azure IoT Hub Device SDK for Python, you can download and run the [iothub_client_sample.py][lnk-client-sample].</span></span>

<span data-ttu-id="dac28-188">Чтобы продолжить знакомство с центром IoT и изучить другие сценарии IoT, см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="dac28-188">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="dac28-189">[Подключение устройства к Azure IoT][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="dac28-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="dac28-190">[How to get started with device management (Node)][lnk-device-management] (Начало работы с управлением устройствами (Node))</span><span class="sxs-lookup"><span data-stu-id="dac28-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="dac28-191">[Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Приступая к работе с архитектурой Azure IoT Edge в Linux)</span><span class="sxs-lookup"><span data-stu-id="dac28-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="dac28-192">Сведения о том, как расширить решение для Интернета вещей и обрабатывать сообщения, отправляемые с устройства в облако в большом количестве, см. [здесь][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="dac28-192">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
