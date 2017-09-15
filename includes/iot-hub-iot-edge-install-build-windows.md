## <a name="install-the-prerequisites"></a><span data-ttu-id="ca1c2-101">Установка необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="ca1c2-101">Install the prerequisites</span></span>

1. <span data-ttu-id="ca1c2-102">Установите [Visual Studio 2015 или Visual Studio 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="ca1c2-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="ca1c2-103">Вы можете использовать бесплатный выпуск Visual Studio Community, если требования к лицензированию выполнены.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-103">You can use the free Community Edition if you meet the licensing requirements.</span></span> <span data-ttu-id="ca1c2-104">Не забудьте добавить Visual C++ и диспетчер пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-104">Be sure to include Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="ca1c2-105">Установите [Git](http://www.git-scm.com) и запустите файл git.exe из командной строки.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from the command line.</span></span>

1. <span data-ttu-id="ca1c2-106">Установите [CMake](https://cmake.org/download/) и запустите файл cmake.exe из командной строки.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from the command line.</span></span> <span data-ttu-id="ca1c2-107">Рекомендуется использовать CMake 3.7.2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="ca1c2-108">В Windows проще всего использовать установщик **MSI**.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-108">The **.msi** installer is the easiest option on Windows.</span></span> <span data-ttu-id="ca1c2-109">Добавьте CMake в PATH по крайней мере для текущего пользователя при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-109">Add CMake to the PATH for at least the current user when the installer prompts you.</span></span>

1. <span data-ttu-id="ca1c2-110">Установите [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="ca1c2-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="ca1c2-111">Добавьте Python в переменную среды `PATH`, последовательно выбрав **Панель управления -> Система -> Дополнительные параметры системы -> Переменные среды**.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-111">Make sure you add Python to your `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="ca1c2-112">В командной строке выполните следующую команду, чтобы клонировать репозиторий GitHub Azure IoT Edge на локальный компьютер:</span><span class="sxs-lookup"><span data-stu-id="ca1c2-112">At a command prompt, run the following command to clone the Azure IoT Edge GitHub repository to your local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-to-build-the-sample"></a><span data-ttu-id="ca1c2-113">Сборка примера</span><span class="sxs-lookup"><span data-stu-id="ca1c2-113">How to build the sample</span></span>

<span data-ttu-id="ca1c2-114">Теперь на локальном компьютере можно создать примеры и среду выполнения IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-114">You can now build the IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="ca1c2-115">Откройте командную строку разработчика для **VS 2015** или **VS 2017**.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="ca1c2-116">Перейдите в корневую папку в локальной копии репозитория **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-116">Navigate to the root folder in your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="ca1c2-117">Запустите скрипт сборки:</span><span class="sxs-lookup"><span data-stu-id="ca1c2-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="ca1c2-118">Этот сценарий создает файл решения Visual Studio выполняет сборку решения.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-118">This script creates a Visual Studio solution file and builds the solution.</span></span> <span data-ttu-id="ca1c2-119">Решение Visual Studio находится в папке **build** локальной копии репозитория **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-119">You can find the Visual Studio solution in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="ca1c2-120">Добавьте параметр `--run-unittests`, чтобы создавать и выполнять модульные тесты.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-120">If you want to build and run the unit tests, add the `--run-unittests` parameter.</span></span> <span data-ttu-id="ca1c2-121">Добавьте параметр `--run-e2e-tests`, чтобы создавать и выполнять сквозные тесты.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-121">If you want to build and run the end to end tests, add the `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="ca1c2-122">При каждом запуске скрипт **build.cmd** удаляет и заново создает папку **build** в корневой папке локальной копии репозитория **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="ca1c2-122">Every time you run the **build.cmd** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **iot-edge** repository.</span></span>