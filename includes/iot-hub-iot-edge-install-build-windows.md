## <a name="install-hello-prerequisites"></a><span data-ttu-id="78a70-101">Установка необходимых компонентов hello</span><span class="sxs-lookup"><span data-stu-id="78a70-101">Install hello prerequisites</span></span>

1. <span data-ttu-id="78a70-102">Установите [Visual Studio 2015 или Visual Studio 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="78a70-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="78a70-103">Можно использовать hello освободить Community Edition, если выполняются требования лицензирования hello.</span><span class="sxs-lookup"><span data-stu-id="78a70-103">You can use hello free Community Edition if you meet hello licensing requirements.</span></span> <span data-ttu-id="78a70-104">Быть tooinclude убедиться, что Visual C++ и диспетчер пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="78a70-104">Be sure tooinclude Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="78a70-105">Установка [git](http://www.git-scm.com) и убедитесь, что git.exe можно запустить из командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="78a70-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from hello command line.</span></span>

1. <span data-ttu-id="78a70-106">Установка [CMake](https://cmake.org/download/) и убедитесь, что cmake.exe можно запустить из командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="78a70-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from hello command line.</span></span> <span data-ttu-id="78a70-107">Рекомендуется использовать CMake 3.7.2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="78a70-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="78a70-108">Hello **.msi** установщик — наиболее простой вариант hello в Windows.</span><span class="sxs-lookup"><span data-stu-id="78a70-108">hello **.msi** installer is hello easiest option on Windows.</span></span> <span data-ttu-id="78a70-109">Добавить CMake toohello путь для по крайней мере hello текущего пользователя при запросе hello установщика.</span><span class="sxs-lookup"><span data-stu-id="78a70-109">Add CMake toohello PATH for at least hello current user when hello installer prompts you.</span></span>

1. <span data-ttu-id="78a70-110">Установите [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="78a70-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="78a70-111">Убедитесь, что добавление Python tooyour `PATH` переменной среды в **панель управления -> Система -> Дополнительно системные параметры "->" переменные среды**.</span><span class="sxs-lookup"><span data-stu-id="78a70-111">Make sure you add Python tooyour `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="78a70-112">В командной строке выполните hello, следующая команда tooclone hello Azure IoT Edge GitHub репозитория tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="78a70-112">At a command prompt, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="78a70-113">Как toobuild hello образца</span><span class="sxs-lookup"><span data-stu-id="78a70-113">How toobuild hello sample</span></span>

<span data-ttu-id="78a70-114">Теперь можно построить hello IoT Edge среды выполнения и образцов на локальном компьютере:</span><span class="sxs-lookup"><span data-stu-id="78a70-114">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="78a70-115">Откройте командную строку разработчика для **VS 2015** или **VS 2017**.</span><span class="sxs-lookup"><span data-stu-id="78a70-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="78a70-116">Перейдите в корневую папку toohello в локальной копии hello **iot edge** репозитория.</span><span class="sxs-lookup"><span data-stu-id="78a70-116">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="78a70-117">Запустите скрипт сборки:</span><span class="sxs-lookup"><span data-stu-id="78a70-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="78a70-118">Этот сценарий создает файл решения Visual Studio и сборка решения hello.</span><span class="sxs-lookup"><span data-stu-id="78a70-118">This script creates a Visual Studio solution file and builds hello solution.</span></span> <span data-ttu-id="78a70-119">Hello решения Visual Studio можно найти в hello **построения** папки в локальной копии hello **iot edge** репозитория.</span><span class="sxs-lookup"><span data-stu-id="78a70-119">You can find hello Visual Studio solution in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="78a70-120">Toobuild и выполнять модульные тесты hello, добавить hello `--run-unittests` параметра.</span><span class="sxs-lookup"><span data-stu-id="78a70-120">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="78a70-121">Toobuild и выполнения тестов tooend окончания hello, добавить hello `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="78a70-121">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="78a70-122">Каждый раз при выполнении hello **build.cmd** сценария, удаляет и затем повторно создает hello **построения** папку в корневой папке hello ваша локальная копия hello **iot edge** репозитория.</span><span class="sxs-lookup"><span data-stu-id="78a70-122">Every time you run hello **build.cmd** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
