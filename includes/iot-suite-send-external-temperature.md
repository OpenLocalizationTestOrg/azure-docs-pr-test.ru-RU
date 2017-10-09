## <a name="configure-hello-nodejs-simulated-device"></a>Настройка устройства имитацию hello Node.js
1. Щелкните hello удаленного мониторинга, **+ добавить устройство** и добавьте *настраиваемые параметры устройства*. Запишите hello центра IoT имя узла, идентификатор устройства и ключ устройства. Они необходимы далее в этом учебнике, при подготовке hello remote_monitoring.js устройства клиентское приложение.
2. Убедитесь, что на компьютере разработки установлен компонент Node.js 0.12.x или более поздняя версия. Запустите `node --version` в командной строке или в версии hello toocheck оболочки. Сведения об использовании пакета диспетчера tooinstall Node.js в Linux см. в разделе [установки Node.js через диспетчер пакетов][node-linux].
3. После установки Node.js клонировать hello последнюю версию hello [azure iot — пакет SDK для узлов] [ lnk-github-repo] компьютер для разработки tooyour репозитория. Всегда используйте hello **master** ветвь для hello последнюю версию библиотек hello и образцы.
4. Из локальной копии hello [azure iot — пакет SDK для узлов] [ lnk-github-repo] репозитория, hello копии, следующие два файла из hello узел или устройство и образцы tooan пустой папки на компьютере разработки:
   
   * packages.json
   * remote_monitoring.js
5. Откройте файл remote_monitoring.js hello и искать hello после определения переменной:
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. Замените **[IoT Hub device connection string]** строкой подключения устройства. Используйте hello значения для имени узла, идентификатор устройства и ключ устройства, записанных на шаге 1 центр IoT. Строка подключения устройства имеет hello следующий формат:
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    Если имя узла вашего центра IoT **contoso** и ИД устройства **mydevice**, строка соединения выглядит как следующий фрагмент кода hello:
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Сохраните файл hello. Запустите следующие команды в консоль или командную строку в папке hello, содержащей эти tooinstall файлы hello необходимые пакеты hello, а затем запустите пример приложения hello:
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a>Наблюдение динамической телеметрии в действии
Hello панели мониторинга отображаются hello температуры и влажности телеметрии с устройств, имитация существующих hello:

![панель мониторинга по умолчанию Hello][image1]

При выборе имитированное устройство Node.js hello, которые выполнялись в предыдущем разделе hello появляется температура, влажность и температура телеметрии:

![Добавление панели мониторинга toohello температура][image2]

решение для удаленного мониторинга Hello автоматически определяет тип телеметрии дополнительных внешних температуры hello и добавляет toohello диаграммы на панели мониторинга hello.

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png