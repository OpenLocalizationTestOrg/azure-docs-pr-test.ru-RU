## <a name="build-iot-edge"></a><span data-ttu-id="0b254-101">Создание Edge Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="0b254-101">Build IoT Edge</span></span>

<span data-ttu-id="0b254-102">В этом руководстве используются пользовательские модули Edge Интернета вещей для связи с предварительно настроенным решением для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="0b254-102">This tutorial uses custom IoT Edge modules to communicate with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="0b254-103">Поэтому модули Edge Интернета вещей нужно создать на основе исходного пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="0b254-103">Therefore, you need to build the IoT Edge modules from custom source code.</span></span> <span data-ttu-id="0b254-104">В следующих разделах описывается, как установить Edge Интернета вещей и создать пользовательский модуль Edge Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="0b254-104">The following sections describe how to install IoT Edge and build the custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="0b254-105">Установка Edge Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="0b254-105">Install IoT Edge</span></span>

<span data-ttu-id="0b254-106">Далее представлены сведения о том, как установить предварительно скомпилированное программное обеспечение Edge Интернета вещей на Intel NUC:</span><span class="sxs-lookup"><span data-stu-id="0b254-106">The following steps describe how to install the pre-compiled IoT Edge software on the Intel NUC:</span></span>

1. <span data-ttu-id="0b254-107">Настройте необходимые репозитории Smart Package, выполнив в Intel NUC следующие команды:</span><span class="sxs-lookup"><span data-stu-id="0b254-107">Configure the required smart package repositories by running the following commands on the Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="0b254-108">Введите `y`, получив от команды запрос **Include this channel?** (Включить этот канал?).</span><span class="sxs-lookup"><span data-stu-id="0b254-108">Enter `y` when the command prompts you to **Include this channel?**.</span></span>

1. <span data-ttu-id="0b254-109">Обновите Smart Package Manager, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0b254-109">Update the smart package manager by running the following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="0b254-110">Установите пакет Edge Интернета вещей Azure, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0b254-110">Install the Azure IoT Edge package by running the following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="0b254-111">Проверьте установку, запустив пример Hello World.</span><span class="sxs-lookup"><span data-stu-id="0b254-111">Verify the installation by running the "Hello world" sample.</span></span> <span data-ttu-id="0b254-112">Этот пример записывает сообщение Hello World в файл log.txt каждые пять секунд.</span><span class="sxs-lookup"><span data-stu-id="0b254-112">This sample writes a hello world message to the log.txT file every five seconds.</span></span> <span data-ttu-id="0b254-113">Запустите пример Hello World, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="0b254-113">The following commands run the "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="0b254-114">При остановке примера игнорируйте все сообщения **Недопустимый аргумент**.</span><span class="sxs-lookup"><span data-stu-id="0b254-114">Ignore any **invalid argument** messages when you stop the sample.</span></span>

    <span data-ttu-id="0b254-115">Вы можете просмотреть содержимое файла журнала, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0b254-115">Use the following command to view the contents of the log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="0b254-116">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="0b254-116">Troubleshooting</span></span>

<span data-ttu-id="0b254-117">Перезагрузите Intel NUC, если отображается сообщение об ошибке No package provides util-linux-dev (Нет пакета, предоставляющего util-linux-dev).</span><span class="sxs-lookup"><span data-stu-id="0b254-117">If you receive the error "No package provides util-linux-dev", try rebooting the Intel NUC.</span></span>
