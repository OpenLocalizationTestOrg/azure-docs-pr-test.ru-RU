## <a name="install-hello-prerequisites"></a>Установка необходимых компонентов hello

1. Установите [Visual Studio 2015 или Visual Studio 2017](https://www.visualstudio.com). Можно использовать hello освободить Community Edition, если выполняются требования лицензирования hello. Быть tooinclude убедиться, что Visual C++ и диспетчер пакетов NuGet.

1. Установка [git](http://www.git-scm.com) и убедитесь, что git.exe можно запустить из командной строки hello.

1. Установка [CMake](https://cmake.org/download/) и убедитесь, что cmake.exe можно запустить из командной строки hello. Рекомендуется использовать CMake 3.7.2 или более поздней версии. Hello **.msi** установщик — наиболее простой вариант hello в Windows. Добавить CMake toohello путь для по крайней мере hello текущего пользователя при запросе hello установщика.

1. Установите [Python 2.7](https://www.python.org/downloads/release/python-27). Убедитесь, что добавление Python tooyour `PATH` переменной среды в **панель управления -> Система -> Дополнительно системные параметры "->" переменные среды**.

1. В командной строке выполните hello, следующая команда tooclone hello Azure IoT Edge GitHub репозитория tooyour локального компьютера.

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a>Как toobuild hello образца

Теперь можно построить hello IoT Edge среды выполнения и образцов на локальном компьютере:

1. Откройте командную строку разработчика для **VS 2015** или **VS 2017**.

1. Перейдите в корневую папку toohello в локальной копии hello **iot edge** репозитория.

1. Запустите скрипт сборки:

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

Этот сценарий создает файл решения Visual Studio и сборка решения hello. Hello решения Visual Studio можно найти в hello **построения** папки в локальной копии hello **iot edge** репозитория. Toobuild и выполнять модульные тесты hello, добавить hello `--run-unittests` параметра. Toobuild и выполнения тестов tooend окончания hello, добавить hello `--run-e2e-tests`.

> [!NOTE]
> Каждый раз при выполнении hello **build.cmd** сценария, удаляет и затем повторно создает hello **построения** папку в корневой папке hello ваша локальная копия hello **iot edge** репозитория.
