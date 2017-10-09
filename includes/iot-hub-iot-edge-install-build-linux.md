## <a name="install-hello-prerequisites"></a><span data-ttu-id="52311-101">Установка необходимых компонентов hello</span><span class="sxs-lookup"><span data-stu-id="52311-101">Install hello prerequisites</span></span>

<span data-ttu-id="52311-102">Hello шагах в этом учебнике предполагается, что вы используете Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="52311-102">hello steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="52311-103">Откройте оболочку и выполните hello следующие пакеты необходимых компонентов hello tooinstall команды:</span><span class="sxs-lookup"><span data-stu-id="52311-103">Open a shell and run hello following commands tooinstall hello prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="52311-104">В оболочке hello выполните hello, следующая команда tooclone hello Azure IoT Edge GitHub репозитория tooyour локального компьютера:</span><span class="sxs-lookup"><span data-stu-id="52311-104">In hello shell, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="52311-105">Как toobuild hello образца</span><span class="sxs-lookup"><span data-stu-id="52311-105">How toobuild hello sample</span></span>

<span data-ttu-id="52311-106">Теперь можно построить hello IoT Edge среды выполнения и образцов на локальном компьютере:</span><span class="sxs-lookup"><span data-stu-id="52311-106">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="52311-107">Откройте оболочку.</span><span class="sxs-lookup"><span data-stu-id="52311-107">Open a shell.</span></span>

1. <span data-ttu-id="52311-108">Перейдите в корневую папку toohello в локальной копии hello **iot edge** репозитория.</span><span class="sxs-lookup"><span data-stu-id="52311-108">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="52311-109">Запустите скрипт сборки:</span><span class="sxs-lookup"><span data-stu-id="52311-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="52311-110">Этот скрипт использует **cmake** toocreate программа папка **построения** в корневой папке hello ваша локальная копия **iot edge** репозитория и создания файла makefile.</span><span class="sxs-lookup"><span data-stu-id="52311-110">This script uses the **cmake** utility toocreate a folder called **build** in hello root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="52311-111">сценарий Hello затем сборка решения hello, пропуск модульные тесты и тесты tooend end.</span><span class="sxs-lookup"><span data-stu-id="52311-111">hello script then builds hello solution, skipping unit tests and end tooend tests.</span></span> <span data-ttu-id="52311-112">Toobuild и выполнять модульные тесты hello, добавить hello `--run-unittests` параметра.</span><span class="sxs-lookup"><span data-stu-id="52311-112">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="52311-113">Toobuild и выполнения тестов tooend окончания hello, добавить hello `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="52311-113">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="52311-114">Каждый раз при выполнении hello **build.sh** сценария, удаляет и затем повторно создает hello **построения** папку в корневой папке hello ваша локальная копия hello **iot edge** репозитория.</span><span class="sxs-lookup"><span data-stu-id="52311-114">Every time you run hello **build.sh** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
