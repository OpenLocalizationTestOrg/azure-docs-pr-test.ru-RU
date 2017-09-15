> [!div class="op_single_selector"]
> * [<span data-ttu-id="0533e-101">Linux</span><span class="sxs-lookup"><span data-stu-id="0533e-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="0533e-102">Windows</span><span class="sxs-lookup"><span data-stu-id="0533e-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="0533e-103">В этой статье содержится пошаговое руководство по [примеру кода Hello World][lnk-helloworld-sample] и демонстрируются основные компоненты архитектуры [Edge Интернета вещей Azure][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="0533e-103">This article provides a detailed walkthrough of the [Hello World sample code][lnk-helloworld-sample] to illustrate the fundamental components of the [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="0533e-104">В примере Edge Интернета вещей Azure используется для сборки простого шлюза, который каждые пять секунд записывает в файл сообщение Hello World.</span><span class="sxs-lookup"><span data-stu-id="0533e-104">The sample uses the Azure IoT Edge to build a simple gateway that logs a "hello world" message to a file every five seconds.</span></span>

<span data-ttu-id="0533e-105">В этом руководстве рассматриваются следующие темы.</span><span class="sxs-lookup"><span data-stu-id="0533e-105">This walkthrough covers:</span></span>

* <span data-ttu-id="0533e-106">**Архитектура примера Hello World**: здесь описано, каким образом [сведения об архитектуре Azure IoT Edge][lnk-edge-concepts] относятся к примеру Hello World и как компоненты работают вместе.</span><span class="sxs-lookup"><span data-stu-id="0533e-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply to the Hello World sample and how the components fit together.</span></span>
* <span data-ttu-id="0533e-107">**Сборка примера**: шаги, необходимые для сборки образца.</span><span class="sxs-lookup"><span data-stu-id="0533e-107">**How to build the sample**: The steps required to build the sample.</span></span>
* <span data-ttu-id="0533e-108">**Запуск примера**: шаги, необходимые для запуска образца.</span><span class="sxs-lookup"><span data-stu-id="0533e-108">**How to run the sample**: The steps required to run the sample.</span></span> 
* <span data-ttu-id="0533e-109">**Типовые выходные данные**: пример выходных данных, ожидаемых при выполнении примера.</span><span class="sxs-lookup"><span data-stu-id="0533e-109">**Typical output**: An example of the output to expect when you run the sample.</span></span>
* <span data-ttu-id="0533e-110">**Фрагменты кода.** Коллекция фрагментов кода, показывающая, каким образом пример Hello World реализует основные компоненты шлюза Edge Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="0533e-110">**Code snippets**: A collection of code snippets to show how the Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="0533e-111">Архитектура примера hello World</span><span class="sxs-lookup"><span data-stu-id="0533e-111">Hello World sample architecture</span></span>
<span data-ttu-id="0533e-112">Пример Hello World иллюстрирует основные понятия, описанные в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="0533e-112">The Hello World sample illustrates the concepts described in the previous section.</span></span> <span data-ttu-id="0533e-113">Пример Hello World реализует шлюз Edge Интернета вещей с конвейером, который состоит из двух модулей Edge Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="0533e-113">The Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="0533e-114">Модуль *Hello World* создает сообщение каждые пять секунд и передает его в модуль ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="0533e-114">The *hello world* module creates a message every five seconds and passes it to the logger module.</span></span>
* <span data-ttu-id="0533e-115">Модуль *ведения журнала* записывает полученные сообщения в файл.</span><span class="sxs-lookup"><span data-stu-id="0533e-115">The *logger* module writes the messages it receives to a file.</span></span>

![Архитектура примера приложения Hello World, созданного с помощью Edge Интернета вещей Azure][4]

<span data-ttu-id="0533e-117">Как описано в предыдущем разделе, модуль Hello World не передает сообщения непосредственно в модуль ведения журнала каждые пять секунд.</span><span class="sxs-lookup"><span data-stu-id="0533e-117">As described in the previous section, the Hello World module does not pass messages directly to the logger module every five seconds.</span></span> <span data-ttu-id="0533e-118">Вместо этого он каждые пять секунд публикует сообщение в брокер.</span><span class="sxs-lookup"><span data-stu-id="0533e-118">Instead, it publishes a message to the broker every five seconds.</span></span>

<span data-ttu-id="0533e-119">Модуль ведения журнала получает сообщение из брокера и обрабатывают его, записывая содержимое сообщения в файл.</span><span class="sxs-lookup"><span data-stu-id="0533e-119">The logger module receives the message from the broker and acts upon it, writing the contents of the message to a file.</span></span>

<span data-ttu-id="0533e-120">Модуль ведения журнала только обрабатывает сообщения из брокера и никогда не публикует сообщения в брокер.</span><span class="sxs-lookup"><span data-stu-id="0533e-120">The logger module only consumes messages from the broker, it never publishes new messages to the broker.</span></span>

![Брокер направляет сообщения между модулями в пакете Edge Интернета вещей Azure][5]

<span data-ttu-id="0533e-122">На представленной выше схеме показана архитектура примера Hello World и относительные пути к исходными файлам, которые реализуют различные части примера в [репозитории][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="0533e-122">The figure above shows the architecture of the Hello World sample and the relative paths to the source files that implement different portions of the sample in the [repository][lnk-iot-edge].</span></span> <span data-ttu-id="0533e-123">Изучите код самостоятельно или воспользуйтесь приведенными ниже фрагментами кода для справки.</span><span class="sxs-lookup"><span data-stu-id="0533e-123">Explore the code on your own, or use the code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md