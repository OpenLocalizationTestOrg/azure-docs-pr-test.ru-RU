> [!div class="op_single_selector"]
> * [<span data-ttu-id="c3cdd-101">Linux</span><span class="sxs-lookup"><span data-stu-id="c3cdd-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="c3cdd-102">Windows</span><span class="sxs-lookup"><span data-stu-id="c3cdd-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="c3cdd-103">В этой статье предоставляет Подробное пошаговое руководство по hello [образец кода Hello World] [ lnk-helloworld-sample] tooillustrate hello базовые компоненты hello [Azure IoT Edge] [ lnk-iot-edge] архитектуры.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-103">This article provides a detailed walkthrough of hello [Hello World sample code][lnk-helloworld-sample] tooillustrate hello fundamental components of hello [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="c3cdd-104">Hello образец использует hello Azure IoT Edge toobuild простой шлюза, который входит файл tooa сообщение «hello world» каждые пять секунд.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-104">hello sample uses hello Azure IoT Edge toobuild a simple gateway that logs a "hello world" message tooa file every five seconds.</span></span>

<span data-ttu-id="c3cdd-105">В этом руководстве рассматриваются следующие темы.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-105">This walkthrough covers:</span></span>

* <span data-ttu-id="c3cdd-106">**Hello World пример архитектуры**: описывает как [принципы Azure IoT Edge] [ lnk-edge-concepts] применить Образец Hello World toohello и как взаимодействуют компоненты hello.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply toohello Hello World sample and how hello components fit together.</span></span>
* <span data-ttu-id="c3cdd-107">**Как toobuild hello образец**: hello образец hello toobuild необходимые действия.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-107">**How toobuild hello sample**: hello steps required toobuild hello sample.</span></span>
* <span data-ttu-id="c3cdd-108">**Как toorun hello образец**: hello образец hello toorun необходимые действия.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-108">**How toorun hello sample**: hello steps required toorun hello sample.</span></span> 
* <span data-ttu-id="c3cdd-109">**Обычно результат выполнения**: пример hello вывода tooexpect при запуске образца hello.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-109">**Typical output**: An example of hello output tooexpect when you run hello sample.</span></span>
* <span data-ttu-id="c3cdd-110">**Фрагменты кода**: коллекцию tooshow фрагменты кода, как Образец Hello World hello реализует ключевые компоненты IoT пограничного шлюза.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-110">**Code snippets**: A collection of code snippets tooshow how hello Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="c3cdd-111">Архитектура примера hello World</span><span class="sxs-lookup"><span data-stu-id="c3cdd-111">Hello World sample architecture</span></span>
<span data-ttu-id="c3cdd-112">Образец Hello World Hello иллюстрирует hello основные понятия, описанные в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-112">hello Hello World sample illustrates hello concepts described in hello previous section.</span></span> <span data-ttu-id="c3cdd-113">Образец Hello World Hello реализует IoT шлюзом, имеет конвейер состоит из двух модулей IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-113">hello Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="c3cdd-114">Hello *Здравствуй, мир!* модуль создает сообщение каждые пять секунд и передает его toohello модуль ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-114">hello *hello world* module creates a message every five seconds and passes it toohello logger module.</span></span>
* <span data-ttu-id="c3cdd-115">Hello *средства ведения журнала* сообщений hello модуля записи, он получает файл tooa.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-115">hello *logger* module writes hello messages it receives tooa file.</span></span>

![Архитектура примера приложения Hello World, созданного с помощью Edge Интернета вещей Azure][4]

<span data-ttu-id="c3cdd-117">Как описано в предыдущем разделе hello hello World Hello, модуль не проходит сообщений напрямую toohello средства ведения журнала модуля каждые пять секунд.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-117">As described in hello previous section, hello Hello World module does not pass messages directly toohello logger module every five seconds.</span></span> <span data-ttu-id="c3cdd-118">Вместо этого он публикует посредник toohello сообщений каждые пять секунд.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-118">Instead, it publishes a message toohello broker every five seconds.</span></span>

<span data-ttu-id="c3cdd-119">модуль ведения журнала Hello получает сообщение hello из hello broker и обрабатывают, запись содержимого hello файла tooa сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-119">hello logger module receives hello message from hello broker and acts upon it, writing hello contents of hello message tooa file.</span></span>

<span data-ttu-id="c3cdd-120">модуль ведения журнала Hello потребляет только сообщения от hello брокера, он никогда не публикует новый брокер toohello сообщений.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-120">hello logger module only consumes messages from hello broker, it never publishes new messages toohello broker.</span></span>

![Как hello компонент Service broker перенаправляет сообщения между модулями в Azure IoT Edge][5]

<span data-ttu-id="c3cdd-122">Hello выше рисунке показана hello архитектура Образец Hello World hello и относительные пути hello toohello исходные файлы, которые реализуют различные части образца hello hello [репозитория][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="c3cdd-122">hello figure above shows hello architecture of hello Hello World sample and hello relative paths toohello source files that implement different portions of hello sample in hello [repository][lnk-iot-edge].</span></span> <span data-ttu-id="c3cdd-123">Изучение кода hello самостоятельно или использовать фрагменты кода hello ниже в качестве руководства.</span><span class="sxs-lookup"><span data-stu-id="c3cdd-123">Explore hello code on your own, or use hello code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md