> [!div class="op_single_selector"]
> * [<span data-ttu-id="11b3a-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="11b3a-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="11b3a-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="11b3a-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="11b3a-103">C#</span><span class="sxs-lookup"><span data-stu-id="11b3a-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="11b3a-104">Введение</span><span class="sxs-lookup"><span data-stu-id="11b3a-104">Introduction</span></span>

<span data-ttu-id="11b3a-105">В [Приступая к работе с близнецы устройства центра IoT][lnk-twin-tutorial], вы узнали, как метаданные tooset устройства из решения обратно завершить с помощью *теги*, зарегистрировать устройство ошибки из приложения для устройств с помощью *сообщил свойства*и эти сведения с помощью SQL-подобного языка запросов.</span><span class="sxs-lookup"><span data-stu-id="11b3a-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how tooset device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="11b3a-106">В этом учебнике вы узнаете, как toouse hello hello устройства двойных *требуемого свойства* вместе с *сообщил свойства*, tooremotely Настройка приложений для устройств.</span><span class="sxs-lookup"><span data-stu-id="11b3a-106">In this tutorial, you will learn how toouse hello hello device twin's *desired properties* along with *reported properties*, tooremotely configure device apps.</span></span> <span data-ttu-id="11b3a-107">В частности в этом учебнике показано, как устройство двойных сообщил и нужные свойства многоэтапной конфигурацию приложения устройства и предоставить hello видимость toohello решения конец hello состояние этой операции на всех устройствах.</span><span class="sxs-lookup"><span data-stu-id="11b3a-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide hello visibility toohello solution back end of hello status of this operation across all devices.</span></span> <span data-ttu-id="11b3a-108">Можно найти дополнительные сведения о роли hello конфигураций устройства в [Обзор управления устройствами с центром IoT][lnk-dm-overview].</span><span class="sxs-lookup"><span data-stu-id="11b3a-108">You can find more information regarding hello role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="11b3a-109">На высоком уровне hello решения серверной части toospecify hello требуемой конфигурацией для устройств, управляемых hello, вместо того чтобы отправлять команды благодаря использованию близнецы устройства.</span><span class="sxs-lookup"><span data-stu-id="11b3a-109">At a high level, using device twins enables hello solution back end toospecify hello desired configuration for hello managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="11b3a-110">Этот запрос помещает устройства hello за настройку hello лучшим способом tooupdate его конфигурации (очень важно в сценариях IoT, где hello возможность tooimmediately выполнить определенные команды влияют на условия конкретного устройства), при постоянно reporting toohello решение обратно завершить текущее состояние hello и потенциальных ошибок hello процесса обновления.</span><span class="sxs-lookup"><span data-stu-id="11b3a-110">This puts hello device in charge of setting up hello best way tooupdate its configuration (very important in IoT scenarios where specific device conditions affect hello ability tooimmediately carry out specific commands), while continually reporting toohello solution back end hello current state and potential error conditions of hello update process.</span></span> <span data-ttu-id="11b3a-111">Этот шаблон является инструментального toohello управление большими наборами устройств, как позволяет hello серверной части решения toohave полную видимость hello состояние процесса настройки hello на всех устройствах.</span><span class="sxs-lookup"><span data-stu-id="11b3a-111">This pattern is instrumental toohello management of large sets of devices, as it enables hello solution back end toohave full visibility of hello state of hello configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="11b3a-112">В сценариях, где управление устройствами осуществляется в интерактивном режиме (включение вентилятора с помощью пользовательского приложения), используйте [прямые методы][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="11b3a-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="11b3a-113">В этом учебнике hello решения серверной части конфигурации телеметрии hello целевого устройства и в результате, приложение hello устройства следует tooapply многоступенчатый процесс конфигурации изменения (например, требующих перезагрузки модуль программного обеспечения, какой это Учебник имитирует с простой задержки).</span><span class="sxs-lookup"><span data-stu-id="11b3a-113">In this tutorial, hello solution back end changes hello telemetry configuration of a target device and, as a result of that, hello device app follows a multi-step process tooapply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="11b3a-114">серверной части решения Hello хранит конфигурацию hello в нужные свойства устройства двойных hello hello следующими способами:</span><span class="sxs-lookup"><span data-stu-id="11b3a-114">hello solution back end stores hello configuration in hello device twin's desired properties in hello following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="11b3a-115">Поскольку конфигурации может быть сложные объекты, они обычно назначаются уникальные идентификаторы (хэши или [GUID][lnk-guid]) toosimplify их сравнения.</span><span class="sxs-lookup"><span data-stu-id="11b3a-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) toosimplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="11b3a-116">Hello приложения для устройств сообщает о текущей конфигурации зеркального отображения свойство hello требуемого **telemetryConfig** включается в hello свойства:</span><span class="sxs-lookup"><span data-stu-id="11b3a-116">hello device app reports its current configuration mirroring hello desired property **telemetryConfig** in hello reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="11b3a-117">Обратите внимание, как выводятся hello **telemetryConfig** имеет дополнительное свойство **состояние**, используемые tooreport hello состояние процесса обновления настройки hello.</span><span class="sxs-lookup"><span data-stu-id="11b3a-117">Note how hello reported **telemetryConfig** has an additional property **status**, used tooreport hello state of hello configuration update process.</span></span>

<span data-ttu-id="11b3a-118">При получении нового требуемой конфигурацией приложение hello устройство сообщает ожидает настройки необходимо изменить сведения о hello:</span><span class="sxs-lookup"><span data-stu-id="11b3a-118">When a new desired configuration is received, hello device app reports a pending configuration by changing hello information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="11b3a-119">Затем в дальнейшем, приложение hello устройства сообщит hello успешности этой операции, обновив hello значения свойства.</span><span class="sxs-lookup"><span data-stu-id="11b3a-119">Then, at some later time, hello device app will report hello success or failure of this operation by updating hello above property.</span></span>
<span data-ttu-id="11b3a-120">Обратите внимание на то, как серверной части hello решение способно, в любое время tooquery hello состояние процесса настройки hello на всех устройствах hello.</span><span class="sxs-lookup"><span data-stu-id="11b3a-120">Note how hello solution back end is able, at any time, tooquery hello status of hello configuration process across all hello devices.</span></span>

<span data-ttu-id="11b3a-121">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="11b3a-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="11b3a-122">Создать приложение имитированное устройство, которое получает обновления конфигурации из серверной части решения hello и информирует как *сообщил свойства* hello конфигурации процесса обновления.</span><span class="sxs-lookup"><span data-stu-id="11b3a-122">Create a simulated device app that receives configuration updates from hello solution back end, and reports multiple updates as *reported properties* on hello configuration update process.</span></span>
* <span data-ttu-id="11b3a-123">Создайте приложение на серверной стороне обновлений hello требуемой конфигурацией устройства, которое затем запросы hello процесс обновления конфигурации.</span><span class="sxs-lookup"><span data-stu-id="11b3a-123">Create a back-end app that updates hello desired configuration of a device, and then queries hello configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
