## <a name="view-hello-telemetry"></a>Представление hello телеметрии

Hello Raspberry Pi теперь отправляет данные телеметрии toohello удаленного решение для мониторинга. Hello телеметрии можно просмотреть на панели мониторинга hello решения. Можно также отправлять сообщения tooyour Raspberry Pi из панели мониторинга hello решения.

- Перейдите в панель мониторинга toohello решения.
- Выберите устройство в hello **tooView устройства** раскрывающегося списка.
- Hello телеметрии из hello Raspberry Pi отображает на панели мониторинга hello.

![Отобразить данные телеметрии из hello Raspberry Pi][img-telemetry-display]

## <a name="act-on-hello-device"></a>Действуют на устройстве hello

С панели мониторинга hello решение можно вызывать методы с вашей Raspberry пи. Когда hello Raspberry Pi подключается toohello решение для удаленного мониторинга, она отправляет сведения о методах hello поддерживаемых им.

- В панели мониторинга hello решение, нажмите кнопку **устройств** toovisit hello **устройств** страницы. Выберите ваш Pi Raspberry в hello **список устройств**. Затем выберите **Методы**:

    ![Список устройств на панели мониторинга][img-list-devices]

- На hello **вызвать метод** выберите **LightBlink** в hello **метод** раскрывающегося списка.

- Выберите **InvokeMethod**. Имитатор Hello выводит сообщение hello консоли на hello Raspberry Pi. приложение Hello на hello Raspberry Pi отправляет подтверждение задней toohello решений мониторинга:

    ![Просмотр журнала методов][img-method-history]

- Можно переключиться Индикатор hello и отключать с помощью hello **ChangeLightStatus** метод с **LightStatusValue** значение слишком**1** для на или **0** для off.

> [!WARNING]
> Если оставить hello удаленное наблюдение решение, работающее в учетной записи Azure, взимается плата за hello выполнения задания. Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config]. Удаление hello предварительно настроенное решение из учетной записи Azure, после завершения его использования.


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md