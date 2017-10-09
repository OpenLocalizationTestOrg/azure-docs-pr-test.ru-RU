## <a name="build-iot-edge"></a><span data-ttu-id="3071a-101">Создание Edge Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="3071a-101">Build IoT Edge</span></span>

<span data-ttu-id="3071a-102">В этом учебнике используется пользовательских toocommunicate IoT Edge модулей с удаленного мониторинга предварительно настроенных решений hello.</span><span class="sxs-lookup"><span data-stu-id="3071a-102">This tutorial uses custom IoT Edge modules toocommunicate with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="3071a-103">Поэтому необходимо toobuild hello IoT Edge модули из пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="3071a-103">Therefore, you need toobuild hello IoT Edge modules from custom source code.</span></span> <span data-ttu-id="3071a-104">Привет, в следующих разделах описаны hello как tooinstall IoT края и построения настраиваемого модуля IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="3071a-104">hello following sections describe how tooinstall IoT Edge and build hello custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="3071a-105">Установка Edge Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="3071a-105">Install IoT Edge</span></span>

<span data-ttu-id="3071a-106">Hello следующие шаги описывают как tooinstall hello предварительная компиляция IoT Edge программного обеспечения на hello Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="3071a-106">hello following steps describe how tooinstall hello pre-compiled IoT Edge software on hello Intel NUC:</span></span>

1. <span data-ttu-id="3071a-107">Настройте репозиториев hello требуется смарт-пакета, выполнив следующие команды на hello Intel NUC hello.</span><span class="sxs-lookup"><span data-stu-id="3071a-107">Configure hello required smart package repositories by running hello following commands on hello Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="3071a-108">Введите `y` при hello предлагает слишком**включить этот канал?**.</span><span class="sxs-lookup"><span data-stu-id="3071a-108">Enter `y` when hello command prompts you too**Include this channel?**.</span></span>

1. <span data-ttu-id="3071a-109">Обновление диспетчера hello смарт-пакетов, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="3071a-109">Update hello smart package manager by running hello following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="3071a-110">Установка пакета Azure IoT Edge hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="3071a-110">Install hello Azure IoT Edge package by running hello following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="3071a-111">Проверка установки hello путем выполнения образца hello «Hello world».</span><span class="sxs-lookup"><span data-stu-id="3071a-111">Verify hello installation by running hello "Hello world" sample.</span></span> <span data-ttu-id="3071a-112">В этом образце записывает файл log.txT toohello hello world сообщения каждые пять секунд.</span><span class="sxs-lookup"><span data-stu-id="3071a-112">This sample writes a hello world message toohello log.txT file every five seconds.</span></span> <span data-ttu-id="3071a-113">Hello следующие команды запускают hello Образец «Hello world»:</span><span class="sxs-lookup"><span data-stu-id="3071a-113">hello following commands run hello "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="3071a-114">Пропускать **недопустимый аргумент** сообщений при остановке образец hello.</span><span class="sxs-lookup"><span data-stu-id="3071a-114">Ignore any **invalid argument** messages when you stop hello sample.</span></span>

    <span data-ttu-id="3071a-115">Используйте следующие команды tooview hello содержимое файла журнала hello hello.</span><span class="sxs-lookup"><span data-stu-id="3071a-115">Use hello following command tooview hello contents of hello log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="3071a-116">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="3071a-116">Troubleshooting</span></span>

<span data-ttu-id="3071a-117">При получении ошибки hello» не пакет предоставляет util-linux-dev», попробуйте перезагрузить hello Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="3071a-117">If you receive hello error "No package provides util-linux-dev", try rebooting hello Intel NUC.</span></span>
