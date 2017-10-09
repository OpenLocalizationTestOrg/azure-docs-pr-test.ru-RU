## <a name="create-a-device-identity"></a>Создание удостоверения устройства

В этом разделе, можно использовать инструмент Node.js [explorer центром IOT] [ iot-hub-explorer] toocreate удостоверение устройства в этом учебнике. Идентификаторы устройств чувствительны к регистру.

1. Выполнение следующих hello в среде командной строки:

    `npm install -g iothub-explorer@latest`

1. Выполните следующие команды toologin tooyour концентратора hello. Замена `{iot hub connection string}` с hello была скопирована строка подключения центр IoT:

    `iothub-explorer login "{iot hub connection string}"`

1. Наконец, создайте новое удостоверение устройства вызывается `myDeviceId` командой hello:

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

Запишите строку подключения устройства hello из результата hello. Эта строка подключения устройства используется hello устройства приложения tooconnect tooyour центр IoT как устройство.

![][img-identity]

См. слишком[Приступая к работе с центром IoT] [ lnk-getstarted] tooprogrammatically создавать удостоверения устройства.

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
