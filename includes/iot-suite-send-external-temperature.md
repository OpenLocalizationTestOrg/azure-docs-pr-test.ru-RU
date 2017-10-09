## <a name="configure-hello-nodejs-simulated-device"></a><span data-ttu-id="7002a-101">Настройка устройства имитацию hello Node.js</span><span class="sxs-lookup"><span data-stu-id="7002a-101">Configure hello Node.js simulated device</span></span>
1. <span data-ttu-id="7002a-102">Щелкните hello удаленного мониторинга, **+ добавить устройство** и добавьте *настраиваемые параметры устройства*.</span><span class="sxs-lookup"><span data-stu-id="7002a-102">On hello remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="7002a-103">Запишите hello центра IoT имя узла, идентификатор устройства и ключ устройства.</span><span class="sxs-lookup"><span data-stu-id="7002a-103">Make a note of hello IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="7002a-104">Они необходимы далее в этом учебнике, при подготовке hello remote_monitoring.js устройства клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="7002a-104">You need them later in this tutorial when you prepare hello remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="7002a-105">Убедитесь, что на компьютере разработки установлен компонент Node.js 0.12.x или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="7002a-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="7002a-106">Запустите `node --version` в командной строке или в версии hello toocheck оболочки.</span><span class="sxs-lookup"><span data-stu-id="7002a-106">Run `node --version` at a command prompt or in a shell toocheck hello version.</span></span> <span data-ttu-id="7002a-107">Сведения об использовании пакета диспетчера tooinstall Node.js в Linux см. в разделе [установки Node.js через диспетчер пакетов][node-linux].</span><span class="sxs-lookup"><span data-stu-id="7002a-107">For information about using a package manager tooinstall Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="7002a-108">После установки Node.js клонировать hello последнюю версию hello [azure iot — пакет SDK для узлов] [ lnk-github-repo] компьютер для разработки tooyour репозитория.</span><span class="sxs-lookup"><span data-stu-id="7002a-108">When you have installed Node.js, clone hello latest version of hello [azure-iot-sdk-node][lnk-github-repo] repository tooyour development machine.</span></span> <span data-ttu-id="7002a-109">Всегда используйте hello **master** ветвь для hello последнюю версию библиотек hello и образцы.</span><span class="sxs-lookup"><span data-stu-id="7002a-109">Always use hello **master** branch for hello latest version of hello libraries and samples.</span></span>
4. <span data-ttu-id="7002a-110">Из локальной копии hello [azure iot — пакет SDK для узлов] [ lnk-github-repo] репозитория, hello копии, следующие два файла из hello узел или устройство и образцы tooan пустой папки на компьютере разработки:</span><span class="sxs-lookup"><span data-stu-id="7002a-110">From your local copy of hello [azure-iot-sdk-node][lnk-github-repo] repository, copy hello following two files from hello node/device/samples folder tooan empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="7002a-111">packages.json</span><span class="sxs-lookup"><span data-stu-id="7002a-111">packages.json</span></span>
   * <span data-ttu-id="7002a-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="7002a-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="7002a-113">Откройте файл remote_monitoring.js hello и искать hello после определения переменной:</span><span class="sxs-lookup"><span data-stu-id="7002a-113">Open hello remote_monitoring.js file and look for hello following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="7002a-114">Замените **[IoT Hub device connection string]** строкой подключения устройства.</span><span class="sxs-lookup"><span data-stu-id="7002a-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="7002a-115">Используйте hello значения для имени узла, идентификатор устройства и ключ устройства, записанных на шаге 1 центр IoT.</span><span class="sxs-lookup"><span data-stu-id="7002a-115">Use hello values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="7002a-116">Строка подключения устройства имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="7002a-116">A device connection string has hello following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="7002a-117">Если имя узла вашего центра IoT **contoso** и ИД устройства **mydevice**, строка соединения выглядит как следующий фрагмент кода hello:</span><span class="sxs-lookup"><span data-stu-id="7002a-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like hello following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Сохраните файл hello. <span data-ttu-id="7002a-119">Запустите следующие команды в консоль или командную строку в папке hello, содержащей эти tooinstall файлы hello необходимые пакеты hello, а затем запустите пример приложения hello:</span><span class="sxs-lookup"><span data-stu-id="7002a-119">Run hello following commands in a shell or command prompt in hello folder that contains these files tooinstall hello necessary packages and then run hello sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="7002a-120">Наблюдение динамической телеметрии в действии</span><span class="sxs-lookup"><span data-stu-id="7002a-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="7002a-121">Hello панели мониторинга отображаются hello температуры и влажности телеметрии с устройств, имитация существующих hello:</span><span class="sxs-lookup"><span data-stu-id="7002a-121">hello dashboard shows hello temperature and humidity telemetry from hello existing simulated devices:</span></span>

![панель мониторинга по умолчанию Hello][image1]

<span data-ttu-id="7002a-123">При выборе имитированное устройство Node.js hello, которые выполнялись в предыдущем разделе hello появляется температура, влажность и температура телеметрии:</span><span class="sxs-lookup"><span data-stu-id="7002a-123">If you select hello Node.js simulated device you ran in hello previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![Добавление панели мониторинга toohello температура][image2]

<span data-ttu-id="7002a-125">решение для удаленного мониторинга Hello автоматически определяет тип телеметрии дополнительных внешних температуры hello и добавляет toohello диаграммы на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="7002a-125">hello remote monitoring solution automatically detects hello additional external temperature telemetry type and adds it toohello chart on hello dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png