## <a name="typical-output"></a><span data-ttu-id="4081d-101">Типовые выходные данные</span><span class="sxs-lookup"><span data-stu-id="4081d-101">Typical output</span></span>

<span data-ttu-id="4081d-102">Hello пример hello выводимые toohello файла журнала в образце Hello World hello.</span><span class="sxs-lookup"><span data-stu-id="4081d-102">hello following example shows hello output written toohello log file by hello Hello World sample.</span></span> <span data-ttu-id="4081d-103">для удобочитаемости форматирования выходных данных Hello:</span><span class="sxs-lookup"><span data-stu-id="4081d-103">hello output is formatted for legibility:</span></span>

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

## <a name="code-snippets"></a><span data-ttu-id="4081d-104">Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="4081d-104">Code snippets</span></span>

<span data-ttu-id="4081d-105">В этом разделе рассматриваются некоторые ключевые разделы кода hello в hello hello\_образец world.</span><span class="sxs-lookup"><span data-stu-id="4081d-105">This section discusses some key sections of hello code in hello hello\_world sample.</span></span>

### <a name="iot-edge-gateway-creation"></a><span data-ttu-id="4081d-106">Создание шлюза Edge Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="4081d-106">IoT Edge gateway creation</span></span>

<span data-ttu-id="4081d-107">Необходимо реализовать *процесс шлюза*.</span><span class="sxs-lookup"><span data-stu-id="4081d-107">You must implement a *gateway process*.</span></span> <span data-ttu-id="4081d-108">Эта программа создает hello внутренней инфраструктуры (hello брокер), загружает модули IoT Edge hello и настраивает процесса шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="4081d-108">This program creates hello internal infrastructure (hello broker), loads hello IoT Edge modules, and configures hello gateway process.</span></span> <span data-ttu-id="4081d-109">Предоставляет hello край IoT **шлюза\_создать\_из\_JSON** функции tooenable toobootstrap шлюза из JSON-файла.</span><span class="sxs-lookup"><span data-stu-id="4081d-109">IoT Edge provides hello **Gateway\_Create\_From\_JSON** function tooenable you toobootstrap a gateway from a JSON file.</span></span> <span data-ttu-id="4081d-110">toouse hello **шлюза\_создать\_из\_JSON** функции, передать его hello путь tooa JSON файла, который определяет hello tooload модули IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="4081d-110">toouse hello **Gateway\_Create\_From\_JSON** function, pass it hello path tooa JSON file that specifies hello IoT Edge modules tooload.</span></span>

<span data-ttu-id="4081d-111">Hello кода можно найти в hello процесс шлюза hello *Hello World* в hello [main.c] [ lnk-main-c] файла.</span><span class="sxs-lookup"><span data-stu-id="4081d-111">You can find hello code for hello gateway process in hello *Hello World* sample in hello [main.c][lnk-main-c] file.</span></span> <span data-ttu-id="4081d-112">Для удобочитаемости hello следующий фрагмент кода показывает сокращенную версию кода процесса шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="4081d-112">For legibility, hello following snippet shows an abbreviated version of hello gateway process code.</span></span> <span data-ttu-id="4081d-113">Эта программа создает шлюз, а затем ждет hello пользователя toopress hello **ввод** ключа перед его разрушает hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="4081d-113">This example program creates a gateway and then waits for hello user toopress hello **ENTER** key before it tears down hello gateway.</span></span>

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

<span data-ttu-id="4081d-114">файл параметров JSON Hello содержит список модулей tooload IoT Edge и hello ссылки между модулями hello.</span><span class="sxs-lookup"><span data-stu-id="4081d-114">hello JSON settings file contains a list of IoT Edge modules tooload and hello links between hello modules.</span></span> <span data-ttu-id="4081d-115">Каждый модуль Edge Интернета вещей должен содержать:</span><span class="sxs-lookup"><span data-stu-id="4081d-115">Each IoT Edge module must specify a:</span></span>

* <span data-ttu-id="4081d-116">**имя**: уникальное имя для модуля "hello".</span><span class="sxs-lookup"><span data-stu-id="4081d-116">**name**: a unique name for hello module.</span></span>
* <span data-ttu-id="4081d-117">**Загрузчик**: загрузчик, который знает, как tooload hello требуемого модуля.</span><span class="sxs-lookup"><span data-stu-id="4081d-117">**loader**: a loader that knows how tooload hello desired module.</span></span> <span data-ttu-id="4081d-118">Загрузчики являются точкой расширения для загрузки разных типов модулей.</span><span class="sxs-lookup"><span data-stu-id="4081d-118">Loaders are an extension point for loading different types of modules.</span></span> <span data-ttu-id="4081d-119">IoT Edge предоставляет загрузчики для модулей, написанных на машинном коде C, Node.js, Java и .Net.</span><span class="sxs-lookup"><span data-stu-id="4081d-119">IoT Edge provides loaders for use with modules written in native C, Node.js, Java, and .NET.</span></span> <span data-ttu-id="4081d-120">Образец Hello World Hello использует собственный загрузчик C hello только из-за все модули hello в этом образце динамической библиотеки, написанные на языке C. Дополнительные сведения о том, как toouse IoT Edge модули, написанные на разных языках см hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), или [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) образцов.</span><span class="sxs-lookup"><span data-stu-id="4081d-120">hello Hello World sample only uses hello native C loader because all hello modules in this sample are dynamic libraries written in C. For more information about how toouse IoT Edge modules written in different languages, see hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) samples.</span></span>
    * <span data-ttu-id="4081d-121">**имя**: hello имя загрузчика hello используется модуль tooload hello.</span><span class="sxs-lookup"><span data-stu-id="4081d-121">**name**: hello name of hello loader used tooload hello module.</span></span>
    * <span data-ttu-id="4081d-122">**entrypoint**: hello путь toohello библиотека, содержащая модуль hello.</span><span class="sxs-lookup"><span data-stu-id="4081d-122">**entrypoint**: hello path toohello library containing hello module.</span></span> <span data-ttu-id="4081d-123">Для Linux эта библиотека представлена SO-файлом, а для Windows — DLL-файлом.</span><span class="sxs-lookup"><span data-stu-id="4081d-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span></span> <span data-ttu-id="4081d-124">точка входа Hello — тип определенного toohello загрузчика используется.</span><span class="sxs-lookup"><span data-stu-id="4081d-124">hello entry point is specific toohello type of loader being used.</span></span> <span data-ttu-id="4081d-125">Hello точки входа загрузчика Node.js — это файл .js.</span><span class="sxs-lookup"><span data-stu-id="4081d-125">hello Node.js loader entry point is a .js file.</span></span> <span data-ttu-id="4081d-126">Hello точки входа загрузчика Java — путь к классам и имя класса.</span><span class="sxs-lookup"><span data-stu-id="4081d-126">hello Java loader entry point is a classpath and a class name.</span></span> <span data-ttu-id="4081d-127">Hello точки входа загрузчика .NET является имя сборки и имя класса.</span><span class="sxs-lookup"><span data-stu-id="4081d-127">hello .NET loader entry point is an assembly name and a class name.</span></span>

* <span data-ttu-id="4081d-128">**args**: необходимо, чтобы все конфигурации модуль hello сведения.</span><span class="sxs-lookup"><span data-stu-id="4081d-128">**args**: any configuration information hello module needs.</span></span>

<span data-ttu-id="4081d-129">Следующий код показывает hello JSON используется toodeclare все Hello hello IoT Edge модули для образца Hello World hello в Linux.</span><span class="sxs-lookup"><span data-stu-id="4081d-129">hello following code shows hello JSON used toodeclare all hello IoT Edge modules for hello Hello World sample on Linux.</span></span> <span data-ttu-id="4081d-130">Требует ли модуль аргументов зависит от структуры hello модуля "hello".</span><span class="sxs-lookup"><span data-stu-id="4081d-130">Whether a module requires any arguments depends on hello design of hello module.</span></span> <span data-ttu-id="4081d-131">В этом примере hello средства ведения журнала модуля принимает аргумент, который является hello путь toohello выходного файла и hello hello\_world модуль не имеет аргументов.</span><span class="sxs-lookup"><span data-stu-id="4081d-131">In this example, hello logger module takes an argument that is hello path toohello output file and hello hello\_world module has no arguments.</span></span>

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

<span data-ttu-id="4081d-132">Hello JSON-файл также содержит ссылки hello между модулями hello, передаваемые toohello брокера.</span><span class="sxs-lookup"><span data-stu-id="4081d-132">hello JSON file also contains hello links between hello modules that are passed toohello broker.</span></span> <span data-ttu-id="4081d-133">Ссылка имеет два свойства:</span><span class="sxs-lookup"><span data-stu-id="4081d-133">A link has two properties:</span></span>

* <span data-ttu-id="4081d-134">**источник**: имя модуля из hello `modules` разделе или `\*`.</span><span class="sxs-lookup"><span data-stu-id="4081d-134">**source**: a module name from hello `modules` section, or `\*`.</span></span>
* <span data-ttu-id="4081d-135">**Приемник**: имя модуля из hello `modules` раздела.</span><span class="sxs-lookup"><span data-stu-id="4081d-135">**sink**: a module name from hello `modules` section.</span></span>

<span data-ttu-id="4081d-136">Каждая ссылка определяет маршрут и направление сообщения.</span><span class="sxs-lookup"><span data-stu-id="4081d-136">Each link defines a message route and direction.</span></span> <span data-ttu-id="4081d-137">Сообщения от hello **источника** модуля доставки toohello **приемник** модуля.</span><span class="sxs-lookup"><span data-stu-id="4081d-137">Messages from hello **source** module are delivered toohello **sink** module.</span></span> <span data-ttu-id="4081d-138">Можно задать hello **источника** модуля слишком`\*`, указывающая, что hello **приемник** модуль получает сообщения от любого модуля.</span><span class="sxs-lookup"><span data-stu-id="4081d-138">You can set hello **source** module too`\*`, which indicates that hello **sink** module receives messages from any module.</span></span>

<span data-ttu-id="4081d-139">Hello код отображает hello JSON используется tooconfigure связи между hello модули, используемые в hello hello\_образец world в Linux.</span><span class="sxs-lookup"><span data-stu-id="4081d-139">hello following code shows hello JSON used tooconfigure links between hello modules used in hello hello\_world sample on Linux.</span></span> <span data-ttu-id="4081d-140">Каждое сообщение, созданное hello `hello_world` модуля используется hello `logger` модуля.</span><span class="sxs-lookup"><span data-stu-id="4081d-140">Every message produced by hello `hello_world` module is consumed by hello `logger` module.</span></span>

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a><span data-ttu-id="4081d-141">Публикация сообщений модуля hello\_world</span><span class="sxs-lookup"><span data-stu-id="4081d-141">Hello\_world module message publishing</span></span>

<span data-ttu-id="4081d-142">Можно найти hello код, используемый hello hello\_сообщений toopublish модуль world hello [«hello_world.c»] [ lnk-helloworld-c] файла.</span><span class="sxs-lookup"><span data-stu-id="4081d-142">You can find hello code used by hello hello\_world module toopublish messages in hello ['hello_world.c'][lnk-helloworld-c] file.</span></span> <span data-ttu-id="4081d-143">Hello следующий фрагмент кода показывает измененные версии кода hello с комментариями и обработка кода, удаленных для удобочитаемости ошибок:</span><span class="sxs-lookup"><span data-stu-id="4081d-143">hello following snippet shows an amended version of hello code with comments added and some error handling code removed for legibility:</span></span>

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

### <a name="helloworld-module-message-processing"></a><span data-ttu-id="4081d-144">Обработка сообщений модуля hello\_world</span><span class="sxs-lookup"><span data-stu-id="4081d-144">Hello\_world module message processing</span></span>

<span data-ttu-id="4081d-145">Hello hello\_world модуля никогда не обрабатывает сообщения, публикации, другие модули IoT Edge toohello брокера.</span><span class="sxs-lookup"><span data-stu-id="4081d-145">hello hello\_world module never processes messages that other IoT Edge modules publish toohello broker.</span></span> <span data-ttu-id="4081d-146">Таким образом, hello реализации обратного вызова сообщение hello в hello hello\_world модуль — это функция холостой.</span><span class="sxs-lookup"><span data-stu-id="4081d-146">Therefore, hello implementation of hello message callback in hello hello\_world module is a no-op function.</span></span>

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a><span data-ttu-id="4081d-147">Публикация и обработка сообщений модуля ведения журнала</span><span class="sxs-lookup"><span data-stu-id="4081d-147">Logger module message publishing and processing</span></span>

<span data-ttu-id="4081d-148">средства ведения журнала модуля Hello получает сообщения от компонента broker hello и записывает их tooa файла.</span><span class="sxs-lookup"><span data-stu-id="4081d-148">hello logger module receives messages from hello broker and writes them tooa file.</span></span> <span data-ttu-id="4081d-149">Он никогда не публикует сообщения.</span><span class="sxs-lookup"><span data-stu-id="4081d-149">It never publishes any messages.</span></span> <span data-ttu-id="4081d-150">Таким образом, код hello hello средства ведения журнала модуля никогда не вызывает hello **Broker_Publish** функции.</span><span class="sxs-lookup"><span data-stu-id="4081d-150">Therefore, hello code of hello logger module never calls hello **Broker_Publish** function.</span></span>

<span data-ttu-id="4081d-151">Hello **Logger_Receive** функции hello [logger.c] [ lnk-logger-c] файл является broker hello hello обратного вызова вызывает toodeliver сообщения toohello средства ведения журнала модуля.</span><span class="sxs-lookup"><span data-stu-id="4081d-151">hello **Logger_Receive** function in hello [logger.c][lnk-logger-c] file is hello callback hello broker invokes toodeliver messages toohello logger module.</span></span> <span data-ttu-id="4081d-152">Hello следующий фрагмент кода показывает измененные версии с комментариями и обработка кода, удаленных для удобочитаемости ошибок:</span><span class="sxs-lookup"><span data-stu-id="4081d-152">hello following snippet shows an amended version with comments added and some error handling code removed for legibility:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4081d-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4081d-153">Next steps</span></span>

<span data-ttu-id="4081d-154">В этой статье вы запускали простой IoT Edge шлюз, который записывает файл журнала tooa сообщений.</span><span class="sxs-lookup"><span data-stu-id="4081d-154">In this article, you ran a simple IoT Edge gateway that writes messages tooa log file.</span></span> <span data-ttu-id="4081d-155">см. пример, который отправляет сообщения tooIoT концентратора, toorun [IoT край, отправляете сообщения из устройства в облако с имитации устройства с помощью Linux] [ lnk-gateway-simulated-linux] или [IoT край, отправлять сообщения с устройства в облако с Имитация устройства, с помощью Windows][lnk-gateway-simulated-windows].</span><span class="sxs-lookup"><span data-stu-id="4081d-155">toorun a sample that sends messages tooIoT Hub, see [IoT Edge – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated-linux] or [IoT Edge – send device-to-cloud messages with a simulated device using Windows][lnk-gateway-simulated-windows].</span></span>


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md