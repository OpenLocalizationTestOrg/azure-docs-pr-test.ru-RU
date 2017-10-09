## <a name="create-a-device-identity"></a><span data-ttu-id="bc789-101">Создание удостоверения устройства</span><span class="sxs-lookup"><span data-stu-id="bc789-101">Create a device identity</span></span>

<span data-ttu-id="bc789-102">В этом разделе, можно использовать инструмент Node.js [explorer центром IOT] [ iot-hub-explorer] toocreate удостоверение устройства в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="bc789-102">In this section, you use a Node.js tool called [iothub-explorer][iot-hub-explorer] toocreate a device identity for this tutorial.</span></span> <span data-ttu-id="bc789-103">Идентификаторы устройств чувствительны к регистру.</span><span class="sxs-lookup"><span data-stu-id="bc789-103">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="bc789-104">Выполнение следующих hello в среде командной строки:</span><span class="sxs-lookup"><span data-stu-id="bc789-104">Run hello following in your command-line environment:</span></span>

    `npm install -g iothub-explorer@latest`

1. <span data-ttu-id="bc789-105">Выполните следующие команды toologin tooyour концентратора hello.</span><span class="sxs-lookup"><span data-stu-id="bc789-105">Then, run hello following command toologin tooyour hub.</span></span> <span data-ttu-id="bc789-106">Замена `{iot hub connection string}` с hello была скопирована строка подключения центр IoT:</span><span class="sxs-lookup"><span data-stu-id="bc789-106">Substitute `{iot hub connection string}` with hello IoT Hub connection string you previously copied:</span></span>

    `iothub-explorer login "{iot hub connection string}"`

1. <span data-ttu-id="bc789-107">Наконец, создайте новое удостоверение устройства вызывается `myDeviceId` командой hello:</span><span class="sxs-lookup"><span data-stu-id="bc789-107">Finally, create a new device identity called `myDeviceId` with hello command:</span></span>

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

<span data-ttu-id="bc789-108">Запишите строку подключения устройства hello из результата hello.</span><span class="sxs-lookup"><span data-stu-id="bc789-108">Make a note of hello device connection string from hello result.</span></span> <span data-ttu-id="bc789-109">Эта строка подключения устройства используется hello устройства приложения tooconnect tooyour центр IoT как устройство.</span><span class="sxs-lookup"><span data-stu-id="bc789-109">This device connection string is used by hello device app tooconnect tooyour IoT Hub as a device.</span></span>

![][img-identity]

<span data-ttu-id="bc789-110">См. слишком[Приступая к работе с центром IoT] [ lnk-getstarted] tooprogrammatically создавать удостоверения устройства.</span><span class="sxs-lookup"><span data-stu-id="bc789-110">Refer too[Getting started with IoT Hub][lnk-getstarted] tooprogrammatically create device identities.</span></span>

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
