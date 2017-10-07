---
title: "aaaGet работы с управлением устройства Azure IoT Hub (.NET или узел) | Документы Microsoft"
description: "Как tooinitiate управления устройства Azure IoT Hub toouse перезагрузите удаленного устройства. Использовать устройства Azure IoT hello пакета SDK для Node.js tooimplement приложение имитированное устройство, которое включает прямой метод и hello Azure IoT служба пакета SDK для .NET tooimplement приложение службы, которое вызывает метод прямой hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: ea6d50dfac1c222d7836e3bf5503c6c9b8c89dfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-netnode"></a>Приступая к работе с управлением устройствами (.NET или Node)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

В этом учебнике описаны следующие процедуры.

* Используйте hello Azure портала toocreate центр IoT и создать удостоверение устройства в концентратор IoT.
* Создание приложения для имитации устройства с прямым методом, который позволяет выполнить перезагрузку устройства. Прямой методы вызываются из облака hello.
* Создайте консольное приложение .NET, которое вызывает метод прямой перезагрузки hello в приложение hello имитированное устройство через концентратор IoT.

В конце этого учебника hello у вас есть приложение Node.js консоли устройства и консольного приложения серверной части .NET (C#):

**dmpatterns_getstarted_device.js**, который подключает центра IoT tooyour с идентификатором hello устройства, созданный ранее, получает прямой метод перезагрузки, имитирует перезагрузка физического и отчеты hello время последней перезагрузки hello.

**TriggerReboot**, прямой метод которого вызывает в приложение hello имитированное устройство, отображает ответ hello, и отображает hello обновлены данные свойства.

toocomplete этого учебника требуется hello следующие:

* Visual Studio 2015 или Visual Studio 2017.
* Node.js версии 0.12.x или более поздней. <br/>  [Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall Node.js для этого учебника в Windows или Linux.
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Триггер удаленной перезагрузки на устройстве hello, с помощью прямой метод
В этом разделе вы создадите консольное приложение .NET (с помощью C#), которое инициирует удаленное обновление устройства с помощью прямого метода. приложение Hello использует устройство двойных запросы toodiscover hello время последней перезагрузки для этого устройства.

1. В Visual Studio добавьте новое решение tooa проекта Visual C# Windows классического с помощью hello **консольного приложения (.NET Framework)** шаблона проекта. Убедитесь, что hello версии платформы .NET Framework 4.5.1 или более поздней версии. Имя проекта hello **TriggerReboot**.

    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]

2. В обозревателе решений щелкните правой кнопкой мыши hello **TriggerReboot** проекта, а затем нажмите кнопку **управление пакетами NuGet**.
3. В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **microsoft.azure.devices**выберите **установить** tooinstall Hello **Microsoft.Azure.Devices** пакета и примите условия использования hello. Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.

    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
4. Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. Добавьте следующие поля toohello hello **программы** класса. Замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello и hello целевое устройство.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. Добавьте следующий метод toohello hello **программы** класса.  Это двойных код получает hello устройства для перезагрузки устройства и выходы hello hello сообщил свойства.
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. Добавьте следующий метод toohello hello **программы** класса.  Этот код запускает hello перезагрузки на устройстве hello, с помощью прямого метода.

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. Наконец, добавьте следующие строки toohello hello **Main** метод:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. Выполните сборку решения hello.

## <a name="create-a-simulated-device-app"></a>Создание приложения виртуального устройства
В этом разделе вы сделаете следующее:

* Создайте консольное приложение Node.js, которое отвечает tooa прямой метод, вызываемый hello облака
* запустите перезагрузку имитации устройства;
* Используйте hello выводятся свойства tooenable устройствами двойных запросы tooidentify устройства и при их последней перезагрузки

1. Создайте пустую папку с именем **manageddevice**.  В hello **manageddevice** папки, создайте файл package.json, используя следующую команду в командной строке hello.  Примите все значения по умолчанию hello:
   
    ```
    npm init
    ```
2. В командной строке в hello **manageddevice** папку, следующая команда tooinstall hello hello **azure iot устройства** пакета SDK для устройства и **azure-iot устройства mqtt**пакета:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. В текстовом редакторе создайте новый **dmpatterns_getstarted_device.js** файла в hello **manageddevice** папки.
4. Добавьте следующие hello «требовать» операторы в начале hello hello **dmpatterns_getstarted_device.js** файла:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Добавить **connectionString** переменной и использовать его toocreate **клиента** экземпляра.  Замените строку соединения hello строки подключения устройства.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Добавить следующие функции tooimplement hello прямого метода на устройстве hello hello
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. Добавьте следующую hello кода hello подключения tooopen tooyour-центр IoT и запустить прослушиватель прямой метод hello:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. Сохраните и закройте hello **dmpatterns_getstarted_device.js** файла.
   
> [!NOTE]
> простые действия tookeep, этот учебник не реализует никакую политику повтора. В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].


## <a name="run-hello-apps"></a>Запускайте приложения hello
Теперь вы находитесь toorun готовности приложения hello.

1. В командной строке hello в hello **manageddevice** папки, запустите следующие команды toobegin прослушивание прямой метод перезагрузки hello hello.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. Консольное приложение hello выполнения C# **TriggerReboot**. Щелкните правой кнопкой мыши hello **TriggerReboot** проекта, выберите **отладки**и выберите **запустить новый экземпляр**.

3. Появиться hello устройства toohello прямой метод ответа в консоли hello.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/