---
title: "обновление встроенного по aaaDevice с центром IoT Azure (.NET или узел) | Документы Microsoft"
description: "Как обновить toouse управления устройствами в центр IoT Azure tooinitiate микропрограммы устройства. Можно использовать устройства Azure IoT hello пакета SDK для Node.js tooimplement приложения имитированное устройство и hello Azure IoT служба пакета SDK для .NET tooimplement службы приложений, которое вызывает обновление встроенного по hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a>Использование устройства управления tooinitiate обновление встроенного по устройства (.NET или узел)
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Введение
В hello [начало работы с управлением устройствами] [ lnk-dm-getstarted] учебник, вы видели, как toouse hello [двойных устройства] [ lnk-devtwin] и [прямой методы] [ lnk-c2dmethod] tooremotely примитивы перезагрузить устройство. В этом учебнике используется hello же примитивы центр IoT и показано, как toodo-законченный имитируемые обновление встроенного по.  Этот шаблон используется в реализации обновлений встроенного hello для hello [образец реализации устройства Raspberry Pi][lnk-rpi-implementation].

В этом учебнике описаны следующие процедуры.

* Создайте консольное приложение .NET, которое вызывает метод прямой firmwareUpdate hello в приложение hello имитированное устройство через концентратор IoT.
* Создайте приложение виртуального устройства, которое реализует прямой метод **firmwareUpdate**. Этот метод запускает многоэтапный процесс ожидает образ встроенного по toodownload hello, он загружает образ встроенного по hello и наконец применение hello образ встроенного по. Во время каждого этапа обновления hello hello устройство использует hello сообщил свойства tooreport о ходе выполнения.

В конце этого учебника hello у вас есть приложение Node.js консоли устройства и консольного приложения серверной части .NET (C#):

**dmpatterns_fwupdate_service.js**, прямой метод которого вызывает в приложение hello имитированное устройство, отображает ответ hello, и периодически (каждые 500 мс) отображает hello обновлены данные свойства.

**TriggerFWUpdate**, который подключает центра IoT tooyour с идентификатором hello устройства, созданный ранее, получает прямой метод firmwareUpdate, завершит toosimulate многими состояниями процесс обновления встроенного по том числе: ожидание hello образа загрузки, Загрузка нового образа hello и наконец применение образа hello.

toocomplete этого учебника требуется hello следующие:

* Visual Studio 2015 или Visual Studio 2017.
* Node.js версии 0.12.x или более поздней. <br/>  [Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall Node.js для этого учебника в Windows или Linux.
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

Выполните hello [начало работы с управлением устройствами](iot-hub-csharp-node-device-management-get-started.md) статью toocreate ваш центр IoT и получить строки подключения центр IoT.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Вызвать обновление удаленного встроенного по на устройстве hello, с помощью прямой метод
В этом разделе вы создадите консольное приложение .NET (с помощью C#), которое инициирует удаленное обновление встроенного ПО на устройстве. приложение Hello использует прямой метод tooinitiate hello обновления и использует устройство двойных запросы tooperiodically получить состояние hello обновления встроенного по active hello.

1. В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта. Имя проекта hello **TriggerFWUpdate**.

    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]

1. В обозревателе решений щелкните правой кнопкой мыши hello **TriggerFWUpdate** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .
1. В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **microsoft.azure.devices**выберите **установить** tooinstall Hello **Microsoft.Azure.Devices** пакета и примите условия использования hello. Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.

    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
1. Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. Добавьте следующие поля toohello hello **программы** класса. Замените hello несколько значений заполнитель с hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello и hello идентификатор устройства.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. Добавьте следующий метод toohello hello **программы** класса:
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. Добавьте следующий метод toohello hello **программы** класса:

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. Наконец, добавьте следующие строки toohello hello **Main** метод:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. В hello обозревателе решений откройте hello **задать автозагружаемых проектов...**  и убедитесь, что hello **действия** для **TriggerFWUpdate** проект является **запустить**.

1. Выполните сборку решения hello.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Запускайте приложения hello
Теперь вы находитесь toorun готовности приложения hello.

1. В командной строке hello в hello **manageddevice** папки, запустите следующие команды toobegin прослушивание прямой метод перезагрузки hello hello.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. В Visual Studio щелкните правой кнопкой мыши на hello **TriggerFWUpdate** projectRun toohello C# консольное приложение, выберите **отладки** и **запустить новый экземпляр**.

3. Появиться hello устройства toohello прямой метод ответа в консоли hello.

    ![Успешное обновление встроенного ПО][img-fwupdate]

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике используется tootrigger прямой метод удаленного обновления встроенного по на устройстве и используемых hello сообщил свойства toofollow hello ход выполнения обновления встроенного по hello.

toolearn tooextend IoT решения и расписание метод вызывает на нескольких устройствах и разделе hello [расписание и широковещательных задания] [ lnk-tutorial-jobs] учебника.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/