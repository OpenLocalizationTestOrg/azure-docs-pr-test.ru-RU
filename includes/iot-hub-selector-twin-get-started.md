> [!div class="op_single_selector"]
> * [<span data-ttu-id="5784c-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="5784c-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="5784c-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="5784c-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="5784c-103">C#</span><span class="sxs-lookup"><span data-stu-id="5784c-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="5784c-104">Java</span><span class="sxs-lookup"><span data-stu-id="5784c-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="5784c-105">Двойники устройств — это документы JSON, хранящие сведения о состоянии устройства (метаданные, конфигурации и условия).</span><span class="sxs-lookup"><span data-stu-id="5784c-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="5784c-106">Центр IoT сохранение двойных устройства для каждого устройства, которое подключается tooit.</span><span class="sxs-lookup"><span data-stu-id="5784c-106">IoT Hub persists a device twin for each device that connects tooit.</span></span>

<span data-ttu-id="5784c-107">Двойники устройства используются для выполнения следующих действий:</span><span class="sxs-lookup"><span data-stu-id="5784c-107">Use device twins to:</span></span>

* <span data-ttu-id="5784c-108">хранение метаданных устройства из серверной части вашего решения;</span><span class="sxs-lookup"><span data-stu-id="5784c-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="5784c-109">Сведения о текущем состоянии, такие как доступные возможности и условий (например, hello методом подключения используется) отчета в приложении для устройства.</span><span class="sxs-lookup"><span data-stu-id="5784c-109">Report current state information such as available capabilities and conditions (for example, hello connectivity method used) from your device app.</span></span>
* <span data-ttu-id="5784c-110">Синхронизируйте состояние hello длительных рабочих процессов (например, обновления встроенного по и конфигурация) между приложением устройства и приложения серверной части.</span><span class="sxs-lookup"><span data-stu-id="5784c-110">Synchronize hello state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="5784c-111">выполнение запроса метаданных, конфигурации или состояния устройства.</span><span class="sxs-lookup"><span data-stu-id="5784c-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="5784c-112">Двойники устройств используются для синхронизации и выполнения запроса конфигураций или условий устройства.</span><span class="sxs-lookup"><span data-stu-id="5784c-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="5784c-113">Дополнительные сведения о при близнецы toouse устройства можно найти в [понять устройство близнецы][lnk-twins].</span><span class="sxs-lookup"><span data-stu-id="5784c-113">More informations on when toouse device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="5784c-114">Двойники устройств хранятся в Центре Интернета вещей. Они содержат следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="5784c-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="5784c-115">*теги*, метаданные устройства доступен только для серверной части решения hello;</span><span class="sxs-lookup"><span data-stu-id="5784c-115">*tags*, device metadata accessible only by hello solution back end;</span></span>
* <span data-ttu-id="5784c-116">*требуемого свойства*, изменяемые решением hello объекты JSON резервное интерфейса и наблюдаемый объект с приложение hello устройства; и</span><span class="sxs-lookup"><span data-stu-id="5784c-116">*desired properties*, JSON objects modifiable by hello solution back end and observable by hello device app; and</span></span>
* <span data-ttu-id="5784c-117">*отчет свойства*, объекты JSON изменяемые приложением устройства hello и для чтения в серверной части решения hello.</span><span class="sxs-lookup"><span data-stu-id="5784c-117">*reported properties*, JSON objects modifiable by hello device app and readable by hello solution back end.</span></span> <span data-ttu-id="5784c-118">(теги и свойства не могут содержать массивы, но объекты могут быть вложенными).</span><span class="sxs-lookup"><span data-stu-id="5784c-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="5784c-119">Кроме того серверной части hello решения можно запрашивать устройство близнецы основании все hello над данными.</span><span class="sxs-lookup"><span data-stu-id="5784c-119">Additionally, hello solution back end can query device twins based on all hello above data.</span></span>
<span data-ttu-id="5784c-120">См. слишком[понять устройство близнецы] [ lnk-twins] Дополнительные сведения об устройстве близнецы и toohello [язык запросов центра IoT] [ lnk-query] ссылки для запроса.</span><span class="sxs-lookup"><span data-stu-id="5784c-120">Refer too[Understand device twins][lnk-twins] for more information about device twins, and toohello [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="5784c-121">В настоящее время устройство близнецы доступны только из устройств, которые подключаются tooIoT концентратора с помощью протокола MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="5784c-121">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="5784c-122">См. toohello [поддержки MQTT] [ lnk-devguide-mqtt] статье инструкции о том, как приложение toouse tooconvert существующие устройства MQTT.</span><span class="sxs-lookup"><span data-stu-id="5784c-122">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>

<span data-ttu-id="5784c-123">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="5784c-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="5784c-124">Создание серверной части приложения, добавляет *теги* двойных tooa устройства, а приложение имитированное устройство, которое сообщает его подключении канала как *сообщил свойство* на устройстве двойных hello.</span><span class="sxs-lookup"><span data-stu-id="5784c-124">Create a back-end app that adds *tags* tooa device twin, and a simulated device app that reports its connectivity channel as a *reported property* on hello device twin.</span></span>
* <span data-ttu-id="5784c-125">Запрос устройства из серверной части приложения, использующие фильтры на hello теги и свойства, созданные ранее.</span><span class="sxs-lookup"><span data-stu-id="5784c-125">Query devices from your back-end app using filters on hello tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md