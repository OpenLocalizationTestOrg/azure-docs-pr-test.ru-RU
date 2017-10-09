---
title: "пакет SDK устройства Azure IoT aaaThe для C | Документы Microsoft"
description: "Начало работы с устройством Azure IoT hello пакета SDK для C и узнайте, как toocreate приложения для устройств, взаимодействовать с центром IoT."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a>Пакет SDK для устройств Azure IoT для C

Hello **устройств Azure IoT SDK** — набор библиотек, предназначенных toosimplify hello процесс отправки сообщений tooand прием сообщений от hello **центр IoT Azure** службы. Существуют различные виды hello SDK, направив определенной платформе, но в этой статье описывается hello **устройств Azure IoT SDK для C**.

пакет SDK устройства Azure IoT Hello для C записывается в toomaximize переносимости ANSI C (C99). Благодаря этой функции hello toooperate хорошо подходит библиотеки на нескольких платформах и устройствах, особенно в том случае, если к минимуму диска и объем памяти — приоритет.

Существует широкий спектр платформы, на какие hello протестирована SDK (hello в разделе [Azure Certified для каталога устройств IoT](https://catalog.azureiotsuite.com/) подробные сведения). Несмотря на то, что эта статья содержит пошаговые руководства для примера кода, работающих на платформе Windows hello, кода hello, описанных в этой статье будут одинаковыми для hello диапазон поддерживаемых платформ.

В этой статье описывается архитектура toohello устройства Azure IoT hello пакета SDK для C. Он демонстрирует, как библиотека устройств tooinitialize hello, отправки данных tooIoT концентратора и получения сообщений из него. Hello сведения в этой статье, должно быть достаточно tooget работы с использованием пакета SDK для hello, но также предоставляет указатели tooadditional сведения о библиотеках hello.

## <a name="sdk-architecture"></a>Архитектура пакета SDK

Можно найти hello [ **устройств Azure IoT SDK для C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub репозитория и просмотра сведений из hello API в hello [Справочник по C API](https://azure.github.io/azure-iot-sdk-c/index.html).

последнюю версию библиотек hello Hello можно найти в hello **master** ветви hello репозитория:

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* Hello core реализация hello SDK соответствует hello **центром IOT\_клиента** папку, содержащую реализацию hello hello нижний уровень API в hello SDK: hello **IoTHubClient** библиотеки. Hello **IoTHubClient** библиотеки содержит API-интерфейсы, реализация необработанных сообщений для отправки сообщений tooIoT концентратора и получения сообщений из центра IoT. Если вы используете эту библиотеку, вам нужно самостоятельно реализовать сериализацию сообщений. Другие составляющие процесса взаимодействия с Центром Интернета вещей реализуются автоматически.
* Hello **сериализатор** папки содержит вспомогательные функции и образцы, которые показывают, как tooserialize данные перед отправкой с помощью центра IoT tooAzure hello клиентской библиотеки. Использование Hello сериализатор hello не является обязательным и предоставляется для удобства. toouse hello **сериализатор** библиотеки, определить модель, которая указывает данных toosend tooIoT концентратора и hello сообщений hello предполагается, что tooreceive от него. После определения модели hello hello SDK содержит рабочую область API, который позволяет tooeasily работы с устройства в облако и сообщения облака на устройство, не беспокоясь о hello сведения о сериализации. Библиотека Hello зависит от других библиотек открытым исходным кодом, реализующие транспорта с помощью протоколов, таких как MQTT и AMQP.
* Hello **IoTHubClient** библиотеки зависит от других библиотек с открытым исходным кодом:
  * Hello [Azure C Общие программы](https://github.com/Azure/azure-c-shared-utility) библиотеку, которая предоставляет общие функциональные возможности для основных задач (например, строки, обработка списка и операции ввода-ВЫВОДА) на несколько связанных с Azure SDK C.
  * Hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) библиотеку, которая является реализацией клиентского AMQP, оптимизированный для ограниченного ресурсов устройств.
  * Hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) библиотеку, которая является библиотекой общего назначения, реализация протокола MQTT hello и оптимизированный для ограниченного ресурсов устройств.

Эти библиотеки используется проще toounderstand, просмотрев пример кода. Hello в следующих разделах описаны шаги несколько hello образцы приложений, которые включены в пакет SDK для hello. В этом пошаговом руководстве будет предоставлять хорошее вид hello hello уровнях архитектуры hello SDK и API-интерфейсы работают приветствия toohow введение различные функциональные возможности.

## <a name="before-you-run-hello-samples"></a>Перед запуском образцов hello

Перед выполнением примеров hello в пакет SDK устройства Azure IoT hello для языка C, необходимо [создания экземпляра службы центра IoT hello](iot-hub-create-through-portal.md) в вашей подписке Azure. Затем выполните следующие задачи hello.

* Подготовка среды разработки
* получение учетных данных устройства.

### <a name="prepare-your-development-environment"></a>Подготовка среды разработки

Пакеты предоставляются для распространенных платформ (например, NuGet для Windows или apt_get для Debian и Ubuntu) и образцы hello использовать эти пакеты, если оно доступно. В некоторых случаях необходимо hello toocompile пакета SDK для или на устройстве. Toocompile hello SDK см [подготовить среду разработки](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) в репозитории GitHub hello.

tooobtain hello образец кода приложения, загрузить копию hello SDK с сайта GitHub. Получить копию исходного hello из hello **master** ветви hello [репозитории GitHub](https://github.com/Azure/azure-iot-sdk-c).


### <a name="obtain-hello-device-credentials"></a>Получить учетные данные устройства hello

Теперь, когда исходный код образца hello hello Далее самое toodo — tooget набор учетных данных устройства. Для устройств toobe может tooaccess центра IoT необходимо сначала добавить toohello устройство hello реестра удостоверений центр IoT. При добавлении устройства вы получаете набор устройств учетные данные, необходимые для hello устройства toobe может tooconnect toohello центр IoT. Hello образцы приложений, описанные в следующем разделе hello ожидается, что эти учетные данные в форме hello **строка подключения устройства**.

Существует несколько средств toohelp открытым исходным кодом, управлять ваш центр IoT.

* Приложение Windows — [обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).
* Кроссплатформенная программа командной строки Azure на Node.js — [iothub-explorer](https://github.com/azure/iothub-explorer).

В этом учебнике используется графический hello *обозреватель устройств* средства. Можно также использовать hello *explorer центром IOT* средства при желании toouse средство CLI.

Анализатор устройства Hello использует различные функции hello Azure IoT службы библиотеки tooperform на центра IoT, включая добавление устройств. Если вы используете hello устройство обозревателя средство tooadd устройство, вы получаете строку подключения для устройства. Необходимо, чтобы это соединение строка toorun hello образцы приложений.

Если вы не знакомы с помощью средства обозревателя устройства hello, hello следующая процедура описывает способ toouse его tooadd устройства и получение строки подключения устройства.

вспомогательное средство tooinstall hello устройства. в разделе [как toouse hello обозреватель устройств для устройств центра IoT](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).

При запуске программы hello, вы видите этот интерфейс:

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

Введите ваш **строка подключения концентратора IoT** в hello первое поле и нажмите кнопку **обновление**. Этот шаг позволяет настроить средство hello, чтобы его могли взаимодействовать с центром IoT.

При настройке hello центра IoT строку соединения, нажмите кнопку hello **управления** вкладки:

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

Эта вкладка служит для управления hello устройства, зарегистрированные в концентратор IoT.

Создать устройство, щелкнув hello **создать** кнопки. Откроется диалоговое окно с заполненным набором ключей (первичных и вторичных). Введите **идентификатор устройства**, а затем нажмите кнопку **Создать**.

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

При создании устройства hello устройств hello список обновлений с все зарегистрированные hello устройств, включая один только что созданный hello. Если щелкнуть новое устройство правой кнопкой мыши, появится следующее меню:

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

При выборе **Скопируйте строку подключения для выбранного устройства**, строка подключения устройства hello: скопированный toohello буфер обмена. Сохраните копию строки подключения устройств hello. Он нужен, при выполнении hello образцы приложений, описанные в следующих разделах hello.

После завершения hello описанные выше действия, вы готовы toostart выполнение некоторых кода. Оба примера имеют константа вверху hello hello основной исходный файл, позволяющий tooenter строку подключения. Здравствуйте, например, соответствующей строке из hello **центром IOT\_клиента\_пример\_mqtt** приложение имеет следующий вид.

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a>Используйте библиотеку IoTHubClient hello

В пределах hello **центром IOT\_клиента** папки в hello [azure iot-sdk c](https://github.com/azure/azure-iot-sdk-c) репозитория, имеется **образцы** папку, содержащую приложение называется **центром IOT\_клиента\_пример\_mqtt**.

версия Windows Hello hello **центром IOT\_клиента\_пример\_mqtt** приложение hello следующие решения Visual Studio включает в себя:

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> При открытии этого проекта в Visual Studio 2017 г примите hello приглашения tooretarget hello toohello последнюю версию проекта.

Это решение содержит один проект: В этом решении установлено четыре пакета NuGet:

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport.
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.umqtt.

Необходимо всегда hello **Microsoft.Azure.C.SharedUtility** пакета при работе с hello SDK. В этом примере используется протокол MQTT hello, поэтому необходимо включить hello **Microsoft.Azure.umqtt** и **Microsoft.Azure.IoTHub.MqttTransport** пакетов (есть эквивалентный пакеты для AMQP и HTTP ). Поскольку образец hello использует hello **IoTHubClient** библиотеки, необходимо также включить hello **Microsoft.Azure.IoTHub.IoTHubClient** пакет в решении.

Реализация hello для образца приложения hello можно найти в hello **центром IOT\_клиента\_пример\_mqtt.c** исходный файл.

Hello Далее используется этот образец приложения toowalk по также требования toouse hello **IoTHubClient** библиотеки.

### <a name="initialize-hello-library"></a>Инициализировать библиотеку hello

> [!NOTE]
> Перед началом работы с библиотеками hello может потребоваться tooperform некоторые инициализацию в зависимости от платформы. Например если вы планируете Linux toouse AMQP необходимо инициализировать библиотеки OpenSSL hello. Здравствуйте, примеры в hello [репозитории GitHub](https://github.com/Azure/azure-iot-sdk-c) вызов функции программы hello **платформы\_init** при hello запускается клиент и вызовите hello **платформы\_deinit**  функция перед выходом. Эти функции объявляются в файле заголовка platform.h hello. Изучите определения hello этих функций для целевой платформы в hello [репозитория](https://github.com/Azure/azure-iot-sdk-c) toodetermine необходимости tooinclude любой код инициализации платформой в клиентском приложении.

Работа с библиотеками hello toostart сначала выделить дескриптор клиента центр IoT:

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

Вы передаете копию строки подключения устройства hello, полученную по функции toothis средство обозревателя устройства hello. Можно также назначить toouse протокола связи hello. В этом примере используется протокол MQTT, но вы также можете использовать протоколы AMQP и HTTP.

При наличии допустимого **центром IOT\_КЛИЕНТА\_ОБРАБОТКИ**, можно запустить вызов API-интерфейсы toosend hello и получать сообщения tooand из центра IoT.

### <a name="send-messages"></a>Отправка сообщений

Пример приложения Hello устанавливает концентратор IoT tooyour цикла toosend сообщений. Следующий фрагмент кода Hello:

- создает сообщение;
- Добавляет свойство toohello сообщение.
- отправляет сообщение.

Сначала создайте сообщение:

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

Каждый раз при отправке сообщения можно указать функцию обратного вызова tooa ссылку, которая вызывается при отправке данных hello. В этом примере вызывается функция обратного вызова hello **SendConfirmationCallback**. Следующий фрагмент кода Hello показывает эту функцию обратного вызова:

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

Обратите внимание, toohello вызов hello **IoTHubMessage\_Destroy** работать после завершения сообщение hello. Эта функция освобождает hello ресурсы, выделенные во время создания приветственных сообщений.

### <a name="receive-messages"></a>Получение сообщений

Получение сообщения является асинхронной операцией. Сначала необходимо зарегистрировать обратный вызов tooinvoke hello Получив сообщение hello устройства:

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

Последний параметр Hello является toowhatever указателя void, которые нужно. В образце hello, он является целым числом tooan указателя, но это может быть tooa указатель более сложная структура данных. Этот параметр включает hello toooperate функции обратного вызова на общего состояния с вызывающим объектом hello этой функции.

Получив сообщение hello устройства hello зарегистрированного обратного вызова вызывается функция. Эта функция обратного вызова получает следующее:

* Идентификатор сообщения Hello и идентификатора корреляции из приветственное сообщение.
* содержимое сообщения Hello.
* Пользовательские свойства из сообщения hello.

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Используйте hello **IoTHubMessage\_GetByteArray** функция tooretrieve приветственное сообщение, которое является строкой в этом примере.

### <a name="uninitialize-hello-library"></a>Отмена инициализации библиотеки hello

При завершения отправки событий и получении сообщений деинициализацию hello IoT библиотеки. toodo таким образом, выполните следующий вызов функции hello:

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

Этот вызов освободит ресурсы hello, ранее выделенный методом hello **IoTHubClient\_CreateFromConnectionString** функции.

Как видите, он просто toosend и получать сообщения с hello **IoTHubClient** библиотеки. Hello библиотеки hello параметры обрабатываются взаимодействует с центром IoT, включая какие toouse протокола (с точки зрения hello hello разработчика, это параметр конфигурации, простых).

Hello **IoTHubClient** библиотека также предоставляет полный контроль над как данных hello tooserialize устройство отправляет tooIoT концентратора. В некоторых случаях такой уровень управления является преимуществом, но в других это не нужны посвящена toobe в реализации. Если это так hello, можно использовать hello **сериализатор** библиотеку, которая описана в следующем разделе hello.

## <a name="use-hello-serializer-library"></a>Использование библиотеки сериализатор hello

Здравствуйте, по существу **сериализатор** библиотеки располагается в верхней части hello **IoTHubClient** библиотеки в hello SDK. Она использует hello **IoTHubClient** библиотеки для hello базового обмена данными с центра IoT, но он добавляет возможности моделирования, удалите hello нагрузку задач, связанных с сериализацией сообщения hello разработчика. Работу этой библиотеки лучше всего продемонстрировать на примере.

Hello внутри **сериализатор** папки в hello [хранилища azure iot-sdk c](https://github.com/Azure/azure-iot-sdk-c), является **образцы** папку, содержащую приложение называется **simplesample \_mqtt**. версия Windows Hello этот образец содержит hello следующие решения Visual Studio.

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> При открытии этого проекта в Visual Studio 2017 г примите hello приглашения tooretarget hello toohello последнюю версию проекта.

Как и в предыдущем примере hello, это один включает несколько пакетов NuGet:

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport.
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.IoTHub.Serializer
* Microsoft.Azure.umqtt.

Вы уже видели большинство этих пакетов в предыдущем примере hello, но **Microsoft.Azure.IoTHub.Serializer** новые. Этот пакет является обязательным при использовании hello **сериализатор** библиотеки.

Реализация hello пример приложения hello можно найти в hello **simplesample\_mqtt.c** файла.

Hello следующие разделы содержат пошаговые инструкции для hello ключевые элементы в этом примере.

### <a name="initialize-hello-library"></a>Инициализировать библиотеку hello

Работа с hello toostart **сериализатор** библиотеки инициализации hello вызовов API-интерфейсы:

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

Hello вызовов toohello **сериализатор\_init** функция одноразового вызова и инициализирует hello базовой библиотеки. Затем вызовите метод hello **IoTHubClient\_LL\_CreateFromConnectionString** функции, которая является hello же API, как и hello **IoTHubClient** образца. Этот вызов устанавливает строки подключения устройства (этот вызов является также где выбрано протокола hello требуется toouse). Этот образец использует MQTT в качестве транспорта hello, но может использовать AMQP или HTTP.

Наконец, вызовите hello **создать\_МОДЕЛИ\_ЭКЗЕМПЛЯР** функции. **WeatherStation** hello пространства имен модели hello и **ContosoAnemometer** является именем hello hello модели. После создания экземпляра hello модели можно использовать toostart отправки и получения сообщений. Однако это важно toounderstand, какая модель —.

### <a name="define-hello-model"></a>Определение модели hello

Модель в hello **сериализатор** библиотека определяет сообщений hello, устройство может отправлять tooIoT концентратора и hello сообщений, называемую *действия* в моделирования язык, который он может получать hello. Определить модель, используя набор макросов C, как hello **simplesample\_mqtt** образец приложения:

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

Hello **НАЧАТЬ\_пространства ИМЕН** и **окончания\_ИМЕН** макросы обоих перевести пространство имен hello hello модели в качестве аргумента. Что-либо между эти макросы ожидается hello определение модели или моделей и структур данных hello, использующих hello моделей.

В этом примере приведена одна модель с именем **ContosoAnemometer**. Эта модель определяет два блока данных, что устройство может отправлять tooIoT концентратора: **DeviceId** и **WindSpeed**. Она также определяет три действия (сообщения), которые ваше устройство может получить: **TurnFanOn**, **TurnFanOff** и **SetAirResistance**. Каждый элемент данных имеет тип, а каждое действие имеет имя (и при необходимости набор параметров).

данные Hello и действия, определенные в модели hello определить рабочую область API, можно использовать tooIoT сообщения toosend концентратора и отвечать отправляемых toomessages toohello устройства. Лучше всего это показать на примере.

### <a name="send-messages"></a>Отправка сообщений

модель Hello определяет hello данные можно отправить tooIoT концентратора. В этом примере, означает одно из hello два элемента данных, определенного с помощью hello **WITH_DATA** макрос. Существуют несколько шагов, необходимых toosend **DeviceId** и **WindSpeed** центр IoT tooan значения. Во-первых, Hello является tooset hello данных, toosend:

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

Hello модель, определенную ранее позволяет tooset hello значений, установив члены **структуры**. Далее сериализации приветственное сообщение, что нужно toosend:

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

Этот код выполняет сериализацию буфера tooa устройства в облако hello (ссылается **назначения**). Hello код запускает hello **sendMessage** функции tooIoT сообщение hello toosend концентратора:

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


Здравствуйте, второй параметр toolast **IoTHubClient\_LL\_SendEventAsync** имеет функцию обратного вызова tooa ссылку, которая вызывается, когда данные hello успешно отправлен. В образце hello Вот hello функции обратного вызова.

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

Второй параметр Hello — контекст toouser указателя; Hello же указатель передан слишком**IoTHubClient\_LL\_SendEventAsync**. В этом случае hello контекста представляет собой простой счетчик, но он может быть любым способом.

Это все, нет сообщений toosending устройства в облако. Hello только что осталось toocover — как tooreceive сообщений.

### <a name="receive-messages"></a>Получение сообщений

Получение сообщения работает аналогично toohello, как работают сообщения в hello **IoTHubClient** библиотеки. Сначала вам нужно зарегистрировать функцию обратного вызова сообщения:

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

Затем можно написать hello функции обратного вызова, вызываемый при получении сообщения:

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

Этот код представляет собой шаблон--имеет hello одинаково для любого решения. Эта функция получает приветственное сообщение и отвечает за маршрутизацию toohello соответствующую функцию через вызов hello слишком**EXECUTE\_команда**. Hello функция, вызываемая в этот момент зависит от определения hello hello действий в модели.

При определении действия в модели, вы будете необходимые tooimplement функция, которая вызывается, когда устройство получает соответствующее сообщение hello. Например, если модель определяет следующее действие:

```c
WITH_ACTION(SetAirResistance, int, Position)
```

Определите функцию со следующей сигнатурой:

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

Обратите внимание на то, как имя hello hello функции совпадает с именем hello действия hello в модели hello и hello параметры функции hello соответствуют hello параметры, указанные для действий hello. Первый параметр Hello всегда является обязательным и содержит указатель toohello экземпляр модели.

Когда hello устройство получает сообщение, соответствующий данной сигнатуре, вызывается соответствующая функция hello. Таким образом, кроме имеющих tooinclude hello стандартный код из **IoTHubMessage**, получения сообщений является простым определения простую функцию для каждого действия, определенный в модели.

### <a name="uninitialize-hello-library"></a>Отмена инициализации библиотеки hello

При завершения операции отправки данных и получении сообщений деинициализацию hello IoT библиотеки.

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

Каждая из этих трех функций выравнивается hello описанных выше трех функций инициализации. Вызов этих API позволит освободить выделенные ранее ресурсы.

## <a name="next-steps"></a>Дальнейшие действия

В этой статье рассматриваются основы использования библиотек hello в hello hello **устройств Azure IoT SDK для C**. Он предоставлен toounderstand достаточно информации, содержание hello SDK, его архитектуры и как tooget начата работа с hello образцов Windows. Далее статья Hello продолжает hello описание hello SDK объясняя [Дополнительные сведения о библиотеке IoTHubClient hello](iot-hub-device-sdk-c-iothubclient.md).

toolearn Дополнительные сведения о разработке приложений для центра IoT. в разделе hello [пакеты SDK Azure IoT][lnk-sdks].

Изучение возможностей hello центра IoT toofurther см. в разделе:

* [Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
