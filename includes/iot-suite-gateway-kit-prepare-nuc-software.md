## <a name="build-iot-edge"></a>Создание Edge Интернета вещей

В этом учебнике используется пользовательских toocommunicate IoT Edge модулей с удаленного мониторинга предварительно настроенных решений hello. Поэтому необходимо toobuild hello IoT Edge модули из пользовательского кода. Привет, в следующих разделах описаны hello как tooinstall IoT края и построения настраиваемого модуля IoT Edge.

### <a name="install-iot-edge"></a>Установка Edge Интернета вещей

Hello следующие шаги описывают как tooinstall hello предварительная компиляция IoT Edge программного обеспечения на hello Intel NUC.

1. Настройте репозиториев hello требуется смарт-пакета, выполнив следующие команды на hello Intel NUC hello.

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    Введите `y` при hello предлагает слишком**включить этот канал?**.

1. Обновление диспетчера hello смарт-пакетов, выполнив следующую команду hello:

    ```bash
    smart update
    ```

1. Установка пакета Azure IoT Edge hello, выполнив следующую команду hello:

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. Проверка установки hello путем выполнения образца hello «Hello world». В этом образце записывает файл log.txT toohello hello world сообщения каждые пять секунд. Hello следующие команды запускают hello Образец «Hello world»:

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    Пропускать **недопустимый аргумент** сообщений при остановке образец hello.

    Используйте следующие команды tooview hello содержимое файла журнала hello hello.

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a>Устранение неполадок

При получении ошибки hello» не пакет предоставляет util-linux-dev», попробуйте перезагрузить hello Intel NUC.
