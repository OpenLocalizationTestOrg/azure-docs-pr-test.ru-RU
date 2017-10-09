## <a name="typical-output"></a>Типовые выходные данные

Hello пример hello выводимые toohello файла журнала в образце Hello World hello. для удобочитаемости форматирования выходных данных Hello:

```json
[{
    "time": "Mon Apr 11 13:48:07 2016",
    "content": "Log started"
}, {
    "time": "Mon Apr 11 13:48:48 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:48:55 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:01 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:04 2016",
    "content": "Log stopped"
}]
```

## <a name="code-snippets"></a>Фрагменты кода

В этом разделе рассматриваются некоторые ключевые разделы кода hello в hello hello\_образец world.

### <a name="iot-edge-gateway-creation"></a>Создание шлюза Edge Интернета вещей

Необходимо реализовать *процесс шлюза*. Эта программа создает hello внутренней инфраструктуры (hello брокер), загружает модули IoT Edge hello и настраивает процесса шлюза hello. Предоставляет hello край IoT **шлюза\_создать\_из\_JSON** функции tooenable toobootstrap шлюза из JSON-файла. toouse hello **шлюза\_создать\_из\_JSON** функции, передать его hello путь tooa JSON файла, который определяет hello tooload модули IoT Edge.

Hello кода можно найти в hello процесс шлюза hello *Hello World* в hello [main.c] [ lnk-main-c] файла. Для удобочитаемости hello следующий фрагмент кода показывает сокращенную версию кода процесса шлюза hello. Эта программа создает шлюз, а затем ждет hello пользователя toopress hello **ввод** ключа перед его разрушает hello шлюза.

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed toocreate hello gateway from JSON\n");
    }
    else
    {
        printf("gateway successfully created from JSON\n");
        printf("gateway shall run until ENTER is pressed\n");
        (void)getchar();
        Gateway_LL_Destroy(gateway);
    }
    return 0;
}
```

файл параметров JSON Hello содержит список модулей tooload IoT Edge и hello ссылки между модулями hello. Каждый модуль Edge Интернета вещей должен содержать:

* **имя**: уникальное имя для модуля "hello".
* **Загрузчик**: загрузчик, который знает, как tooload hello требуемого модуля. Загрузчики являются точкой расширения для загрузки разных типов модулей. IoT Edge предоставляет загрузчики для модулей, написанных на машинном коде C, Node.js, Java и .Net. Образец Hello World Hello использует собственный загрузчик C hello только из-за все модули hello в этом образце динамической библиотеки, написанные на языке C. Дополнительные сведения о том, как toouse IoT Edge модули, написанные на разных языках см hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), или [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) образцов.
    * **имя**: hello имя загрузчика hello используется модуль tooload hello.
    * **entrypoint**: hello путь toohello библиотека, содержащая модуль hello. Для Linux эта библиотека представлена SO-файлом, а для Windows — DLL-файлом. точка входа Hello — тип определенного toohello загрузчика используется. Hello точки входа загрузчика Node.js — это файл .js. Hello точки входа загрузчика Java — путь к классам и имя класса. Hello точки входа загрузчика .NET является имя сборки и имя класса.

* **args**: необходимо, чтобы все конфигурации модуль hello сведения.

Следующий код показывает hello JSON используется toodeclare все Hello hello IoT Edge модули для образца Hello World hello в Linux. Требует ли модуль аргументов зависит от структуры hello модуля "hello". В этом примере hello средства ведения журнала модуля принимает аргумент, который является hello путь toohello выходного файла и hello hello\_world модуль не имеет аргументов.

```json
"modules" :
[
    {
        "name" : "logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/logger/liblogger.so"
        }
        },
        "args" : {"filename":"log.txt"}
    },
    {
        "name" : "hello_world",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/hello_world/libhello_world.so"
        }
        },
        "args" : null
    }
]
```

Hello JSON-файл также содержит ссылки hello между модулями hello, передаваемые toohello брокера. Ссылка имеет два свойства:

* **источник**: имя модуля из hello `modules` разделе или `\*`.
* **Приемник**: имя модуля из hello `modules` раздела.

Каждая ссылка определяет маршрут и направление сообщения. Сообщения от hello **источника** модуля доставки toohello **приемник** модуля. Можно задать hello **источника** модуля слишком`\*`, указывающая, что hello **приемник** модуль получает сообщения от любого модуля.

Hello код отображает hello JSON используется tooconfigure связи между hello модули, используемые в hello hello\_образец world в Linux. Каждое сообщение, созданное hello `hello_world` модуля используется hello `logger` модуля.

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a>Публикация сообщений модуля hello\_world

Можно найти hello код, используемый hello hello\_сообщений toopublish модуль world hello [«hello_world.c»] [ lnk-helloworld-c] файла. Hello следующий фрагмент кода показывает измененные версии кода hello с комментариями и обработка кода, удаленных для удобочитаемости ошибок:

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" tooa set of message properties that
    // will be appended toohello message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set hello content for hello message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set hello properties for hello message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on hello msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of hello thread*/
        }
        else
        {
            // publish hello message toohello broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a>Обработка сообщений модуля hello\_world

Hello hello\_world модуля никогда не обрабатывает сообщения, публикации, другие модули IoT Edge toohello брокера. Таким образом, hello реализации обратного вызова сообщение hello в hello hello\_world модуль — это функция холостой.

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a>Публикация и обработка сообщений модуля ведения журнала

средства ведения журнала модуля Hello получает сообщения от компонента broker hello и записывает их tooa файла. Он никогда не публикует сообщения. Таким образом, код hello hello средства ведения журнала модуля никогда не вызывает hello **Broker_Publish** функции.

Hello **Logger_Receive** функции hello [logger.c] [ lnk-logger-c] файл является broker hello hello обратного вызова вызывает toodeliver сообщения toohello средства ведения журнала модуля. Hello следующий фрагмент кода показывает измененные версии с комментариями и обработка кода, удаленных для удобочитаемости ошибок:

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get hello message properties from hello message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert hello collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode hello message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start hello construction of hello final string toobe logged by adding
    // hello timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add hello message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add hello content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write hello formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a>Дальнейшие действия

В этой статье вы запускали простой IoT Edge шлюз, который записывает файл журнала tooa сообщений. см. пример, который отправляет сообщения tooIoT концентратора, toorun [IoT край, отправляете сообщения из устройства в облако с имитации устройства с помощью Linux] [ lnk-gateway-simulated-linux] или [IoT край, отправлять сообщения с устройства в облако с Имитация устройства, с помощью Windows][lnk-gateway-simulated-windows].


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md