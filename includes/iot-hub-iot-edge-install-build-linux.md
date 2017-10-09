## <a name="install-hello-prerequisites"></a>Установка необходимых компонентов hello

Hello шагах в этом учебнике предполагается, что вы используете Ubuntu Linux.

Откройте оболочку и выполните hello следующие пакеты необходимых компонентов hello tooinstall команды:

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

В оболочке hello выполните hello, следующая команда tooclone hello Azure IoT Edge GitHub репозитория tooyour локального компьютера:

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a>Как toobuild hello образца

Теперь можно построить hello IoT Edge среды выполнения и образцов на локальном компьютере:

1. Откройте оболочку.

1. Перейдите в корневую папку toohello в локальной копии hello **iot edge** репозитория.

1. Запустите скрипт сборки:

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

Этот скрипт использует **cmake** toocreate программа папка **построения** в корневой папке hello ваша локальная копия **iot edge** репозитория и создания файла makefile. сценарий Hello затем сборка решения hello, пропуск модульные тесты и тесты tooend end. Toobuild и выполнять модульные тесты hello, добавить hello `--run-unittests` параметра. Toobuild и выполнения тестов tooend окончания hello, добавить hello `--run-e2e-tests`.

> [!NOTE]
> Каждый раз при выполнении hello **build.sh** сценария, удаляет и затем повторно создает hello **построения** папку в корневой папке hello ваша локальная копия hello **iot edge** репозитория.
