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
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a>Подключиться с помощью Python концентратор IoT tooyour имитированное устройство
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

В конце этого учебника hello будет иметь два приложения Python:

* **CreateDeviceIdentity.py**, которая создает удостоверения устройства и связана защита ключа tooconnect приложение имитации устройства.
* **SimulatedDevice.py**, который подключает tooyour центр IoT с идентификатором hello устройства, созданный ранее и периодически отправляет данные телеметрии сообщений с помощью протокола MQTT hello.

> [!NOTE]
> статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild toorun обоих приложений на устройствах и серверной части вашего решения.
> 
> 

toocomplete этого учебника требуется hello следующие:

* [Python 2.x или 3.x][lnk-python-download]. Сделать убедиться, что toouse hello 32-разрядная или 64-разрядной установки, необходимые настройки. При появлении запроса во время установки hello сделать убедиться, что переменная среды платформой tooyour tooadd Python. При использовании Python 2.x, может потребоваться слишком[Установка или обновление *pip*, hello Python пакета системы управления][lnk-install-pip].
* При использовании ОС Windows, затем [распространяемого пакета Visual C++] [ lnk-visual-c-redist] tooallow hello использования собственных библиотек DLL из Python.
* [Node.js 4.0 или более поздней версии][lnk-node-download]. Сделать убедиться, что toouse hello 32-разрядная или 64-разрядной установки, необходимые настройки. Это hello необходимые tooinstall [IoT Hub анализатор][lnk-iot-hub-explorer].
* Активная учетная запись Azure. Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

> [!NOTE]
> Hello *pip* пакетов для `azure-iothub-service-client` и `azure-iothub-device-client` в настоящее время доступны только для ОС Windows. Linux и Mac OS, см. разделы Linux и Mac OS определенного toohello на hello [подготовить среду разработки для Python] [ lnk-python-devbox] post.
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Теперь Центр Интернета вещей создан. Используйте hello имя узла Центр IoT и hello центра IoT строку подключения в hello конца данного учебника.

> [!NOTE]
> Концентратор IoT можно также легко создать в командной строке, используя hello Python или Node.js на основе Azure CLI. статья Hello [создать центр IoT с помощью Azure CLI 2.0 hello] [ lnk-azure-cli-hub] hello toodo быстрых действий, поэтому показан. 
> 

## <a name="create-a-device-identity"></a>Создание удостоверения устройства
В этом разделе перечислены шаги hello toocreate Python консольного приложения, который создает удостоверение устройства в реестре удостоверений hello концентратор IoT. Устройства могут подключаться tooIoT концентратора только в том случае, если он имеет запись в реестре удостоверений hello. Дополнительные сведения см. в разделе hello **реестра удостоверений** раздел hello [руководстве для разработчиков центра IoT][lnk-devguide-identity]. При запуске это консольное приложение, он создает уникальный идентификатор устройства и ключ, что при отправке устройства в облако, устройство может использовать tooidentify самого сообщения tooIoT концентратора.

1. Откройте командную строку и установить hello **Azure IoT Hub службы SDK для Python**. Закройте командную строку hello, после установки пакета SDK для hello.

    ```
    pip install azure-iothub-service-client
    ```

2. Создайте файл Python с именем **CreateDeviceIdentity.py**. Откройте его в [редактора/IDE Python по своему усмотрению][lnk-python-ide-list], Здравствуйте, например, по умолчанию [IDLE][lnk-idle].

3. Добавьте следующий код tooimport hello необходимые модули из пакета SDK службы hello hello:

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. Добавить hello после кода, заменив заполнитель hello для `[IoTHub Connection String]` со строкой hello подключения для центра IoT hello, созданный в предыдущем разделе hello. Можно использовать любое имя, как hello `DEVICE_ID`.
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. Добавить hello следующие функции tooprint часть сведений об устройстве hello.

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
3. Добавьте следующие функции toocreate hello устройства идентификации с помощью hello диспетчер реестра hello. 

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
4. Наконец добавьте функцию main hello, как показано ниже и сохраните файл hello.

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
5. На hello командной строки, запустите hello **CreateDeviceIdentity.py** следующим образом:

    ```python
    python CreateDeviceIdentity.py
    ```
6. Вы увидите начало создать имитированное устройство hello. Запишите hello **deviceId** и hello **primaryKey** этого устройства. Эти значения должны позже при создании приложения, которое подключается tooIoT концентратора как устройство.

    ![Успешное создание устройства][1]

> [!NOTE]
> Hello реестра удостоверений центра IoT хранится только toohello устройства удостоверения tooenable безопасного доступа центра IoT. Он сохраняет идентификаторы и ключи toouse устройства как учетные данные безопасности и включение или отключение флага, что toodisable доступа можно использовать для отдельных устройств. Если приложению toostore другие метаданные для конкретного устройства, его следует использовать хранилище конкретного приложения. Дополнительные сведения см. в разделе hello [руководстве для разработчиков центра IoT][lnk-devguide-identity].
> 
> 


## <a name="create-a-simulated-device-app"></a>Создание приложения виртуального устройства
В этом разделе перечислены шаги hello toocreate консольное приложение Python, которое имитирует устройство и отправляет сообщения из устройства в облако центра IoT tooyour.

1. Откройте новую командную строку и установите hello Azure IoT Hub устройства SDK для Python следующим образом. Закройте командную строку hello после установки hello.

    ```
    pip install azure-iothub-device-client
    ```
2. Создайте файл с именем **SimulatedDevice.py**. Откройте его в редакторе или интегрированной среде разработки Python (например, IDLE).

3. Добавьте следующую hello необходимые модули кода tooimport из SDK устройства hello hello.

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. Добавить hello следующим кодом и замените заполнитель hello для `[IoTHub Device Connection String]` со строкой hello подключения для вашего устройства. Строка подключения устройства Hello, обычно имеет формат hello объекта `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`. Используйте hello **deviceId** и **primaryKey** hello устройства, созданный в hello предыдущего раздела tooreplace hello `<deviceId>` и `<primaryKey>` соответственно. Замените `<hostName>` именем узла Центра Интернета вещей (обычно это `<IoT hub name>.azure-devices.net`).

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
5. Добавьте следующий код toodefine обратный вызов подтверждения отправки hello. 

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
6. Добавьте следующий код tooinitialize hello устройства клиента hello.

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. Добавьте следующие hello функцией tooformat и отправки сообщения из вашего центра IoT tooyour имитированное устройство.

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
8. Наконец добавьте основной функции hello. 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. Сохраните и закройте hello **SimulatedDevice.py** файла. Вы являются теперь готовы toorun это приложение.

> [!NOTE]
> простые действия tookeep, этот учебник не реализует никакую политику повтора. В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a>Получение сообщений с виртуального устройства
tooreceive телеметрии сообщения с устройства, необходимо toouse [концентраторов событий][lnk-event-hubs-overview]-совместимый конечная точка, предоставляемая hello центра IoT, который считывает сообщения из устройства в облако hello. Чтение hello [Приступая к работе с концентраторами событий] [ lnk-eventhubs-tutorial] учебника сведения о способ tooprocess сообщений из концентраторов событий для конечной точки центра IoT совместимое концентратора событий. Концентраторы событий еще не поддерживает телеметрии в Python, поэтому можно либо создать [Node.js](iot-hub-node-node-getstarted.md#D2C_node) или [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) сообщения консоли на основе концентраторов событий приложения tooread hello устройства в облако из центра IoT. В этом учебнике показано, как можно использовать hello [IoT Hub анализатор] [ lnk-iot-hub-explorer] tooread эти сообщения устройства.

1. Откройте командную строку и установите hello Explorer концентратора IoT. 

    ```
    npm install -g iothub-explorer
    ```

2. Запустите следующую команду в командной строке hello hello, наблюдение за toobegin hello сообщения из устройства в облако с устройства. Использовать центр IoT строку подключения в заполнитель hello после `--login`.

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. Откройте новую командную строку и перейдите в каталог toohello, содержащий hello **SimulatedDevice.py** файла.

4. Запустите hello **SimulatedDevice.py** файл, который периодически отправляет центр IoT tooyour данных телеметрии. 
   
    ```
    python SimulatedDevice.py
    ```
5. Просмотрите сообщения hello устройства на hello командной строки hello Explorer концентратора IoT hello в предыдущем разделе. 

    ![Сообщения Python, отправляемые с устройства в облако][2]

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello. Вы использовали устройства удостоверения tooenable hello имитируемые устройства приложения toosend сообщения из устройства в облако toohello центр IoT. Вы заметили hello сообщений, полученных hello центр IoT с помощью средства обозревателя концентратора IoT hello hello. 

Посетите tooexplore hello Python SDK для использования Azure IoT Hub подробно, [репозиторий Git концентратора][lnk-python-github]. tooreview hello возможности обмена сообщениями hello Azure IoT Hub службы SDK для Python, можно загрузить и запустить [iothub_messaging_sample.py][lnk-messaging-sample]. Для имитации сторона устройства с помощью hello Azure IoT Hub устройства SDK для Python, можно загрузить и запустить hello [iothub_client_sample.py][lnk-client-sample].

Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:

* [Подключение устройства к Azure IoT][lnk-connect-device]
* [How to get started with device management (Node)][lnk-device-management] (Начало работы с управлением устройствами (Node))
* [Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Приступая к работе с архитектурой Azure IoT Edge в Linux)

toolearn tooextend сообщений в масштабе, IoT решение и процесс устройства в облако. в статье hello [обрабатывать сообщения из устройства в облако] [ lnk-process-d2c-tutorial] учебника.
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
